---
title: "bir Azure Automation tümleştirme modülü aaaCreate | Microsoft Docs"
description: "Öğretici, Azure Automation tümleştirme modülleri hello oluşturma, test ve örnek kullanımı aracılığıyla yol göstermektedir."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Azure Automation Tümleştirme Modülleri
PowerShell hello temel Azure Automation'un ardındaki teknolojidir. Azure Automation PowerShell üzerine kurulu olmadığından, PowerShell modülleri Azure Automation'un genişletilmesinde anahtar toohello ' dir. Bu makalede, biz PowerShell modülleri Azure Otomasyonu'nun kullanımını hello özellikleri yönlendirecek, tooas "Tümleştirme modülleri" denir ve bunlar tümleştirme modülü olarak çalışmalarını kendi PowerShell modülleri toomake oluşturmak için en iyi yöntemler Azure Otomasyonu. 

## <a name="what-is-a-powershell-module"></a>PowerShell Modülü nedir?
PowerShell modülü PowerShell cmdlet'leri gibi oluşan bir gruptur **Get-Date** veya **Copy-Item**kullanılabilecek hello PowerShell konsolunu, komut dosyaları, iş akışları, runbook'ları ve gibi PowerShell DSC kaynakları WindowsFeature veya PowerShell DSC kaynaklarından kullanılabilen dosya. PowerShell hello işlevlerin gösterilir cmdlet'ler ve DSC kaynakları ve her cmdlet/DSC kaynağı bir PowerShell modülü tarafından desteklenir, PowerShell ile birlikte birçoğu. Örneğin, hello **Get-Date** cmdlet hello Microsoft.PowerShell.Utility PowerShell modülünün bir parçasıdır ve **Copy-Item** cmdlet hello Microsoft.PowerShell.Management PowerShell modülünün bir parçasıdır ve Merhaba paket DSC kaynağı da PSDesiredStateConfiguration PowerShell modülünün hello bir parçasıdır. Bu modüllerin her ikisi de PowerShell ile birlikte verilir. Ancak çok sayıda PowerShell modülü PowerShell bir parçası olarak bulunmaz ve bunun yerine PowerShell Galerisi gibi yerlerde hello geniş PowerShell topluluğu tarafından veya System Center 2012 Configuration Manager gibi birinci veya üçüncü taraf ürünleri ile dağıtılır.  karmaşık görevleri kapsüllenmiş işlevler aracılığıyla daha basit hale hello modülleri yararlı olur.  Daha fazla bilgiyi [MSDN'de PowerShell modülleri](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx) konusunda bulabilirsiniz. 

## <a name="what-is-an-azure-automation-integration-module"></a>Azure Automation Tümleştirme Modülü nedir?
Tümleştirme Modülü, PowerShell modülünden çok farklı değildir. Kendi isteğe bağlı olarak bir ek dosya - runbook'hello modülün cmdlet'leriyle ile kullanılan bir Azure Otomasyonu bağlantı türü toobe belirten bir meta veri dosyası içeren bir PowerShell modülüdür. İsteğe bağlı dosya olsun veya olmasın bu PowerShell modülleri Azure Otomasyonu toomake kendi cmdlet'leri için kullanılabilir runbook'ları ve kullanılabilir, DSC kaynakları içinde DSC yapılandırmalarında kullanılacak kullanmak içine alınabilir. Merhaba perde arkasında Azure Automation bu modülleri depolar ve runbook işi ve DSC derleme işi yürütme süresinde, bunları burada runbook'ların yürütüldüğü, DSC yapılandırmalarının derlenir hello Azure Automation korumalı alanlarına yükler.  Böylece tooapply DSC yapılandırmaları çalışan makineler bunları çekebilir modüllerdeki DSC kaynakları hello Automation DSC çekme sunucusuna da otomatik olarak yerleştirilir.  

Azure PowerShell modülleri sayısı hello kutusunda Azure Otomasyonu, toouse dışında Azure yönetim hemen başlayabilmeniz ancak ne olursa olsun sistemi, hizmet veya toointegrate ile istediğiniz aracı için PowerShell modülleri içeri aktarabilirsiniz gönderdiğimiz. 

> [!NOTE]
> Belirli modüller "Genel modülleri" Merhaba Otomasyon hizmeti olarak gönderilir. Bu genel modüller, otomatik olarak onları tooyour Otomasyon hesabını iter automation hesabı oluşturma ve bunları bazen güncelleştiriyoruz kullanılabilir tooyou ' dir. Bunları istemiyorsanız toobe otomatik güncelleştirilmiş-her zaman alabilir, hello aynı modülü kendiniz ve hello hizmetinde gönderdiğimiz bu modülü hello genel Modül sürümü, önceliğe sahip olur. 

Tümleştirme modülü paketini içeri aktarma hello aynı adı hello modülü ve bir .zip uzantısı hello sahip sıkıştırılmış bir dosya biçimidir. Merhaba Windows PowerShell modülünü ve hello modülde varsa bildirim dosyası (.psd1) dahil olmak üzere tüm destek dosyalarını içerir.

Merhaba modülü bir Azure Otomasyonu bağlantı türü içermesi gerekiyorsa hello ada sahip bir dosya da içermelidir `<ModuleName>-Automation.json` hello bağlantı türü özelliklerini belirtir. Bu sıkıştırılmış .zip dosyanızın hello modülü klasör içinde yerleştirilen bir json dosyasıdır ve hello alanları içeren bir "bağlantı" gerekli tooconnect toohello sistemi veya hizmet hello modülü temsil eder. Bu sayede Azure Automation’da bağlantı türü oluşturulur. Merhaba alan adları ayarlayabilirsiniz bu dosyayı kullanan türleri, hello alanların şifreli veya hello modülünün hello bağlantı türü için isteğe bağlı olması gerekir. Merhaba, hello json dosyası biçiminde bir şablon verilmiştir:

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Service Management Automation dağıttıysanız ve Otomasyon runbook'larınız için tümleştirme modülü paketleri oluşturulan, bilgili tooyou görünmelidir. 

## <a name="authoring-best-practices"></a>Yazma En İyi Uygulamaları
Tümleştirme modülleri temelde PowerShell modülleri olsa bile yoktur hala pek çok öneririz göz önünde bulundurun toomake bir PowerShell modülü yazarken, Azure Automation'da en kullanışlı. Bunlardan bazıları Azure Automation'a özeldir ve bunlardan bazıları modüllerinizi PowerShell iş akışında iyi iş yararlı yalnızca toomake olduğundan Otomasyon desteklemediğini kullandığınızdan bağımsız olarak. 

1. Merhaba modüldeki her cmdlet için Yardım URI ve bir Özet, açıklama, içerir. PowerShell'de hello ile kullanma hakkında bazı bilgiler cmdlet'leri tooallow hello kullanıcı tooreceive Yardım tanımlayabilirsiniz **Get-Help** cmdlet'i. Örneğin, bir .psm1 dosyasında yazılan PowerShell modülü için bir yardım URI’sını ve özeti nasıl tanımlayacağınız aşağıda anlatılmıştır.<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Bu bilgileri sağlayarak yalnızca gösterilmez hello'ı kullanarak bu Yardım **Get-Help** cmdlet, PowerShell konsolunda Merhaba, ayrıca Azure automation'da bu Yardım işlevinin açığa çıkarır.  Örneğin, runbook yazma sırasında etkinlik eklenirken. "Ayrıntılı Yardımı görüntüleyin" seçeneğinin tıklanması Itanium tabanlı sistemler için açık hello Yardım URI'hello başka bir sekmesinde tooaccess Azure Otomasyonu kullandığınız web tarayıcısında.<br>![Tümleştirme Modülü Yardımı](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Merhaba modül uzak bir sistemle bağlantılı çalıştırıyorsa,

    a. Merhaba bağlantı türü de denir hello gerekli bilgileri tooconnect toothat uzak sistem, tanımlayan bir tümleştirme modülü meta veri dosyası içermelidir.  
    b. Merhaba modüldeki her cmdlet, parametre olarak mümkün tootake bir bağlantı nesnesi (ilgili bağlantı türünün bir örneği) olmalıdır.  

    Merhaba modülündeki cmdlet'leri hello hello bağlantı türü alanlarının sahip bir nesne bir parametre toohello cmdlet'ini olarak geçirme izni verirseniz Azure automation'da daha kolay toouse haline gelir. Bu şekilde, kullanıcılar bir cmdlet'i her çağırdığında hello bağlantı varlık toohello cmdlet'in ilgili parametreleriyle toomap parametreleri yok. Yukarıdaki Hello runbook örneğinde bağlı olarak, bu CorpTwilio tooaccess Twilio adlı bir Twilio bağlantı varlığı kullanır ve hello hesaptaki tüm hello telefon numaraları döndürür.  Merhaba bağlantı toohello parametrelerini hello cmdlet'inin hello alanlarının nasıl eşlendiğini fark ettiniz mi?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Bir ve daha kolay tooapproach bu hello bağlantı nesnesi toohello cmdlet doğrudan geçiyor-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    Cmdlet'lerinizin, cmdlet'leri tooaccept bir bağlantı nesnesini parametrelerin bağlantı alanları yerine bir parametre olarak doğrudan vererek etkinleştirebilirsiniz. Genellikle Azure Automation kullanmayan kullanıcılar cmdlet'lerinizi hashtable tooact hello bağlantı nesnesi olarak oluşturma olmadan çağırabilirsiniz böylece her biri için ayarlanmış bir parametre isteyeceksiniz. Parametre kümesi **SpecifyConnectionFields** kullanılan toopass hello bağlantı alanı özelliklerini tek tek aşağıdadır. **UseConnectionObject** geçirdiğiniz sağlar hello düz ile bağlantı. Gördüğünüz gibi hello içinde Send-TwilioSMS cmdlet'i hello [Twilio PowerShell modülündeki](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) iki şekilde sağlar: 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Hello modüldeki tüm cmdlet'ler için çıktı türünü tanımlayın. Tasarım zamanında IntelliSense'in cmlet'i çıkış türünü tanımlamaya hello belirlemek toohelp yazma sırasında hello cmdlet özelliklerini çıktı. Otomasyon runbook grafik, tasarım zamanı bilgisinin anahtar tooan kolay kullanıcı deneyimi, modülüyle olduğu yazma sırasında özellikle yararlı olur.<br><br> ![Grafik Runbook’u Çıktı Türü](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Bu, benzer bir cmdlet öğesinin toohello "İleri tür" işlevine animasyonun çıktı PowerShell ISE'de toorun gerek kalmadan.<br><br> ![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Merhaba modüldeki cmdlet'ler parametreler için karmaşık nesne türlerini almamalıdır. PowerShell İş Akışı, karmaşık türleri seri durumdan çıkarılmış biçimde depolaması nedeniyle PowerShell’den farklıdır. İlkel türler temel olarak kalır, ancak halde temelde özellik paketi seri durumdan dönüştürülmüş tootheir sürümleri karmaşık türleridir. Örneğin, hello kullandıysanız **Get-Process** cmdlet'i bir runbook (veya bir PowerShell iş akışı bu), bu [Deserialized.System.Diagnostic.Process] türünde bir nesne döndürür, değil, beklenen [hello System.Diagnostic.Process] türü. Bu tür tüm aynı özellikleri çıkarılmamış türle ancak hello yöntemlerin hiçbiri hello gibi hello sahiptir. Ve burada hello cmdlet Bu parametre için [System.Diagnostic.Process] değerini bekler, bir parametre tooa cmdlet'ini olarak, bu değer toopass denerseniz aşağıdaki hata hello alırsınız: *'işlem' parametresinde bağımsız değişken dönüşümü işlenemiyor . Hata: "hello"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process"türündeki"System.Diagnostics.Process (CcmExec)"değeri dönüştürülemiyor.*   Merhaba arasındaki bir tür uyuşmazlığı beklenen [System.Diagnostic.Process] türünü ve verilen [Deserialized.System.Diagnostic.Process] türü hello olduğundan budur. Merhaba bu soruna geçici bir çözüm modülünüzün tooensure hello cmdlet'ler parametreler için karmaşık türler almayan yoludur. Merhaba yanlış şekilde toodo İşte bunu.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    Burada da hello şekilde hello cmdlet tarafından dahili olarak kullanılabilmesi için bir temel alarak toograb karmaşık nesne hello ve bunu kullanın. Merhaba PowerShell bağlamında cmdlet'leri yürütme olduğundan değil PowerShell iş akışı hello cmdlet $process hello doğru [System.Diagnostic.Process] türünü haline gelir.  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Runbook'lardaki bağlantı varlıkları karmaşık bir tür olan hashtable'da olan ve henüz bu hashtable'da cmdlet'lere toobe mümkün toobe göründüğü kendi – bağlantı parametresi mükemmel, herhangi bir cast özel durumu ile. Teknik olarak, bazı PowerShell türleri mümkün toocast kendi serileştirilmiş form seri durumdan tootheir formundan doğru olduğundan ve bu nedenle hello çıkarılmamış türle kabul eden parametrelerde cmdlet'lere geçirilebilir. Hashtable bunlardan biridir. Bir modül yazarının tanımlı türlerinin toobe, bunların düzgün şekilde de seri durumdan şekilde uygulanması mümkündür, ancak bazı dengelemeler tooconsider vardır. türü gereksinimlerini toohave varsayılan bir oluşturucu Merhaba, tüm alt özellikleri ortak ve bir pstypeconverter'ı olması. Ancak, zaten tanımlı türler için o hello modül yazarına desteklemez kendi, Hayır çok "bunları Düzelt", bu nedenle öneri tooavoid parametrelerin tüm karmaşık türler hello yoktur. Runbook yazma İpucu: bazı cmdlet'lerinizi nedenden dolayı tootake karmaşık bir tür parametresi veya başkasının gerektiren bir karmaşık tür parametresi, PowerShell iş akışı runbook'hello geçici çözüm ve PowerShell iş akışları yerel modül kullanıyorsanız Powershell'dir hello karmaşık türü oluşturan toowrap hello cmdlet'ini ve hello hello karmaşık türü tüketen hello cmdlet'i aynı Inlinescript etkinliği. PowerShell iş akışı, hello karmaşık tür oluşturan hello cmdlet doğru türü msgıd yerine Inlinescript içeriğinin PowerShell yürütür. bu yana değil hello karmaşık tür serisi.
5. Tüm cmdlet'ler hello modülünde durum bilgisiz hale getirin. PowerShell iş akışı farklı bir oturumda hello iş akışında çağrılan her cmdlet'i çalışır. Bu, oluşturulan veya diğer Cmdlet'lerde aynı modülü PowerShell iş akışı runbook'larında çalışmaz hello değiştiren oturum durumuna bağlı cmdlet'lerin anlamına gelir.  Örneği ne toodo değil.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. Merhaba modülü tam olarak bir xcopy'ye pakette yer alan. Runbook'ları tooexecute gerektiğinde Azure Automation modülleri dağıtılmış toohello Automation korumalı olduğundan, bunlar çalıştıran hello konak bağımsız olarak toowork ihtiyaç duyar. Bu, hello modülü paketi yukarı mümkün tooZip olması ise tooany taşımak, anlamı başka bir ana bilgisayarı ile aynı veya daha yeni PowerShell sürümü hello ve varsa, Bu konakta PowerShell ortamına içe aktarıldığında da normal çalışmasını. Bu toohappen için sırayla hello modülü değil hello modülü klasörünü (Azure Automation'a içeri aktarırken daraltılmış yukarı hello klasörü) dışındaki tüm dosyalara bağlı veya herhangi bir konaktaki benzersiz kayıt defteri ayarları üzerinde hello tarafından belirlenen gibi bir ürün yükleyin. Bu en iyi uygulama uyulmazsa hello modül Azure Automation'da kullanılamaz.  

## <a name="next-steps"></a>Sonraki adımlar

* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)
* PowerShell modülleri oluşturma hakkında daha fazla toolearn bakın [bir Windows PowerShell modülü yazma](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

