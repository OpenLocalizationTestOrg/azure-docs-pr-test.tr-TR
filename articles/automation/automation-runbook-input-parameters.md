---
title: "aaaRunbook giriş parametreleri | Microsoft Docs"
description: "Runbook giriş parametreleri başlatıldığında toopass veri tooa runbook sağlayarak runbook'ların hello esnekliğini artırır. Bu makalede giriş parametreleri runbook'ları kullanıldığı farklı senaryolar anlatılmaktadır."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Runbook giriş parametreleri
Runbook giriş parametreleri başlatıldığında toopass veri tooit sağlayarak runbook'ların hello esnekliğini artırır. Merhaba parametreler belirli senaryolar ve ortamlar için hedeflenen hello runbook eylemleri toobe olanak tanır. Bu makalede, biz farklı senaryolar üzerinden giriş parametreleri runbook'ları kullanıldığı anlatılmaktadır.

## <a name="configure-input-parameters"></a>Giriş Parametrelerini Yapılandır
Giriş parametreleri PowerShell, PowerShell iş akışı ve grafik runbook'lar yapılandırılabilir. Bir runbook farklı veri türleriyle birden çok parametre ya da hiç parametre hiç olabilir. Giriş parametreleri zorunlu veya isteğe bağlı olabilir ve isteğe bağlı parametreler için varsayılan bir değer atayabilirsiniz. Merhaba kullanılabilir yöntemlerin biri aracılığıyla başlattığınızda, bir runbook'un giriş parametreleri toohello değerler atayabilirsiniz. Bu yöntemler, bir runbook hello portalı veya web hizmeti başlatılıyor içerir. Başka bir runbook'u satır içi olarak adlandırılan bir alt runbook'u olarak da başlatabilirsiniz.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Giriş parametreleri PowerShell ve PowerShell iş akışı runbook'ları yapılandırma
PowerShell ve [PowerShell iş akışı runbook'ları](automation-first-runbook-textual.md) Azure Otomasyonu'nda öznitelikleri aşağıdaki hello tanımlanan giriş parametreleri destekler.  

| **Özellik** | **Açıklama** |
|:--- |:--- |
| Tür |Gereklidir. Merhaba veri türü için Hello parametre değeri bekleniyor. Herhangi bir .NET türü geçerli değil. |
| Ad |Gereklidir. Merhaba parametresinin Hello adı. Bu gerekir hello runbook içinde benzersiz olmalıdır ve yalnızca harf, sayı içeren veya alt çizgi karakterleri. Bir harf ile başlamalıdır. |
| Zorunlu |İsteğe bağlı. Bir değer hello parametresi için sağlanan olup olmadığını belirtir. Bu çok ayarlarsanız,**$true**, sonra da hello runbook başlatılırken bir değer sağlanmalıdır. Bu çok ayarlarsanız,**$false**, sonra da bir değer isteğe bağlıdır. |
| Varsayılan değer |İsteğe bağlı.  Merhaba runbook başlatılırken bir değer değil geçtiyse hello parametresi için kullanılan bir değeri belirtir. Varsayılan değer otomatik olarak hello parametre hello zorunlu ayarı bağımsız olarak isteğe bağlı hale getirir ve herhangi bir parametre için ayarlayabilirsiniz. |

Windows PowerShell giriş parametreleri burada doğrulama gibi diğer adlar, listelenenler ve parametre kümeleri çok daha fazla özniteliklerini destekler. Ancak, Azure Automation şu anda yukarıda listelenen yalnızca hello giriş parametreleri destekler.

PowerShell iş akışı runbook'ları bir parametre tanımı burada birden çok parametre virgülle ayrılır genel form, aşağıdaki hello içeriyor.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Ne zaman tanımladığınız parametreler hello belirtmezseniz **zorunlu** özniteliği sonra varsayılan olarak, hello parametre isteğe bağlı olarak kabul edilir. PowerShell iş akışı runbook'ları bir parametre için varsayılan bir değer ayarlarsanız, ayrıca, bu PowerShell tarafından hello bağımsız olarak isteğe bağlı bir parametre olarak kabul edilecek **zorunlu** öznitelik değeri.
> 
> 

Örnek olarak, sanal makineler, tek bir VM veya bir kaynak grubundaki tüm sanal makineleri ayrıntılarını çıkarır bir PowerShell iş akışı runbook giriş parametreleri hello yapılandıralım. Bu runbook hello ekran aşağıdaki gösterildiği gibi iki parametreye sahiptir: sanal makine ve hello hello kaynak grubunun adını hello adı.

![Automation PowerShell iş akışı](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

Bu parametre tanımında parametreleri hello **$VMName** ve **$resourceGroupName** dize türünde basit parametreleridir. Bununla birlikte, PowerShell ve PowerShell iş akışı runbook'ları tüm basit türleri ve karmaşık türler gibi destek **nesne** veya **PSCredential** giriş parametreleri için.

Runbook'unuz bir nesne türü giriş parametresi varsa, sonra kullanın (adı, değer) içeren bir PowerShell hashtable toopass bir değer çiftleri. Örneğin, bir runbook'ta parametresi aşağıdaki hello varsa:

     [Parameter (Mandatory = $true)]
     [object] $FullName

Ardından değer toohello parametresi aşağıdaki hello geçirebilirsiniz:

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Giriş parametreleri grafik runbook'ları yapılandırma
çok[grafik runbook yapılandırma](automation-first-runbook-graphical.md) giriş parametreleri ile sanal makineleri ayrıntılarını ya da çıkarır bir grafik runbook tek bir VM veya bir kaynak grubundaki tüm sanal makineleri oluşturalım. Bir runbook yapılandırma, aşağıda açıklandığı gibi iki ana etkinliklerini oluşur.

[**Runbook'ları Azure farklı çalıştır hesabıyla kimlik doğrulaması** ](automation-sec-configure-azure-runas-account.md) tooauthenticate Azure ile.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) sanal makinelerin tooget hello özellikleri.

Merhaba kullanabilirsiniz [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) etkinlik toooutput hello adlarını sanal makinelerin. Merhaba etkinlik **Get-AzureRmVm** iki parametre hello kabul **sanal makine adı** ve hello **kaynak grubu adı**. Bu parametreler hello runbook her başlattığınızda farklı değerler gerektirebilir olduğundan, giriş parametreleri tooyour runbook ekleyebilirsiniz. Merhaba adımları tooadd giriş parametreleri şunlardır:

1. Select hello hello grafik runbook'tan **Runbook'lar** dikey ve ardından [ **Düzenle** ](automation-graphical-authoring-intro.md) onu.
2. Merhaba runbook Düzenleyicisi'nden tıklatın **giriş ve çıkış** tooopen hello **giriş ve çıkış** dikey.
   
    ![Otomasyon grafik runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Merhaba **giriş ve çıkış** dikey penceresinde hello runbook için tanımlanan giriş parametreleri listesini görüntüler. Bu dikey penceresinde, yeni bir giriş parametresi eklemek veya var olan bir giriş parametresi hello yapılandırmasını düzenleyin. tooadd hello runbook için yeni bir parametre tıklatın **giriş Ekle** tooopen hello **Runbook giriş parametresi** dikey. Burada, şu parametreler hello yapılandırabilirsiniz:
   
   | **Özellik** | **Açıklama** |
   |:--- |:--- |
   | Ad |Gereklidir.  Merhaba parametresinin Hello adı. Bu gerekir hello runbook içinde benzersiz olmalıdır ve yalnızca harf, sayı içeren veya alt çizgi karakterleri. Bir harf ile başlamalıdır. |
   | Açıklama |İsteğe bağlı. Giriş parametresi hello amacı hakkında açıklama. |
   | Tür |İsteğe bağlı. Merhaba parametre değeri için beklenen veri türü hello. Desteklenen parametre türleri **dize**, **Int32**, **Int64**, **ondalık**, **Boolean**, **DateTime**, ve **nesne**. Bir veri türü seçili değilse, çok varsayılanları**dize**. |
   | Zorunlu |İsteğe bağlı. Bir değer hello parametresi için sağlanan olup olmadığını belirtir. Seçerseniz **Evet**, sonra da hello runbook başlatılırken bir değer sağlanmalıdır. Seçerseniz **hiçbir**, bir değer hello runbook başlatıldığında ve varsayılan bir değer ayarlanabilir gerekli değildir. |
   | Varsayılan değer |İsteğe bağlı. Merhaba runbook başlatılırken bir değer değil geçtiyse hello parametresi için kullanılan bir değeri belirtir. Varsayılan değer, zorunlu olmayan bir parametre için ayarlanabilir. Varsayılan değer, tooset seçin **özel**. Merhaba runbook başlatılırken başka bir değer sağlanmadığı sürece bu değer kullanılır. Seçin **hiçbiri** tooprovide istemiyorsanız, herhangi bir varsayılan değer. |
   
    ![Yeni giriş Ekle](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Merhaba aşağıdaki hello tarafından kullanılacak olan özelliklere sahip iki parametre Oluştur **Get-AzureRmVm** etkinlik:
   
   * **Parametre1:**
     
     * Ad - VMName
     * -Dize türünde
     * Zorunlu - yok
   * **Parametre2:**
     
     * Ad - resourceGroupName
     * -Dize türünde
     * Zorunlu - yok
     * Varsayılan değer - özel
     * Özel varsayılan değer - \<hello sanal makineleri içeren hello kaynak grubu adı >
5. Merhaba parametreleri ekledikten sonra tıklatın **Tamam**.  Bunları artık hello görüntüleyebilirsiniz **giriş ve çıkış dikey**. Tıklatın **Tamam** yeniden ve ardından **kaydetmek** ve **Yayımla** runbook'unuz.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Runbook'ları tooinput parametrelerinde değerler atayın
Runbook'larında senaryoları aşağıdaki hello tooinput parametre değerlerinin geçmesini sağlayabilirsiniz.

### <a name="start-a-runbook-and-assign-parameters"></a>Bir runbook başlatın ve parametreleri atayın
Bir runbook birçok yolu başlatılabilir: hello bir Web kancası ile PowerShell cmdlet'leri ile hello REST API ile veya hello SDK ile Azure portal aracılığıyla. Aşağıda bir runbook'u başlatma ve parametreleri atamak için farklı yöntemler açıklanmaktadır.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Hello Azure portal kullanarak yayımlanan bir runbook başlatın ve parametreleri atayın
Olduğunda, [hello runbook'u başlatmak](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Runbook'u Başlat** dikey penceresi açılır ve yeni oluşturduğunuz hello parametreleri için değerleri yapılandırabilirsiniz.

![Merhaba portalı kullanmaya başlama](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Merhaba giriş kutusu altındaki Hello etiketinde hello parametresi için belirlenen hello öznitelikleri görebilirsiniz. Öznitelikler, zorunlu veya isteğe bağlı, türü ve varsayılan değeri içerir. Merhaba Yardım balonu sonraki toohello parametre adı, parametre giriş değerleri toomake kararlardan gereksinim duyduğunuz tüm hello anahtar bilgileri görebilirsiniz. Bir parametre zorunlu veya isteğe bağlı olup, bu bilgiler içerir. Ayrıca hello türü ve varsayılan değer (varsa) ve diğer yararlı notlar içerir.

![Yardım balonu](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Dize türü parametreleri desteği **boş** dize değerleri.  Girme **[oluşması]** hello giriş parametresi boş dize toohello parametre kutusunu geçer. Ayrıca, dize türü parametreleri desteklemeyen **Null** geçirilen değerleri. Ardından PowerShell herhangi bir değer toohello dize parametre geçirmezseniz boş olarak görürler.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Yayımlanan bir runbook'ta PowerShell cmdlet'lerini kullanarak başlatmak ve parametreleri atayın
* **Azure Resource Manager cmdlet'lerini:** bir kaynak grubunda kullanılarak oluşturulmuş bir Otomasyon runbook'u başlatabilirsiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Örnek:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Azure Hizmet Yönetimi cmdlet'lerini:** bir varsayılan kaynak grubunda kullanılarak oluşturulmuş bir Otomasyon runbook'u başlatabilirsiniz [başlangıç AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Örnek:**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> PowerShell cmdlet'lerini, varsayılan parametre kullanarak bir runbook'u başlattığınızda **MicrosoftApplicationManagementStartedBy** hello değeri ile oluşturulan **PowerShell**. Bu parametre hello görüntüleyebilirsiniz **iş ayrıntıları** dikey.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Bir SDK kullanarak bir runbook'u başlatmak ve parametreleri atayın
* **Azure Resource Manager yöntemi:** hello bir programlama dili SDK kullanarak bir runbook'u başlatabilirsiniz. Otomasyon hesabınızda bir runbook'u başlatmak için C# kod parçacığı aşağıdadır. Tüm hello kodu görüntüleyebilirsiniz bizim [GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Azure hizmet yönetimi yöntemi:** hello bir programlama dili SDK kullanarak bir runbook'u başlatabilirsiniz. Otomasyon hesabınızda bir runbook'u başlatmak için C# kod parçacığı aşağıdadır. Tüm hello kodu görüntüleyebilirsiniz bizim [GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart bu yöntem bir sözlük toostore hello runbook parametreleri oluşturmak **VMName** ve **resourceGroupName**ve değerleri. Daha sonra hello runbook başlatın. Merhaba C# kod parçacığını yukarıda tanımlanan hello yöntemi çağırmak için aşağıdadır.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Merhaba REST API kullanarak bir runbook'u başlatmak ve parametreleri atayın
Bir runbook işi oluşturulur ve Azure Automation REST API hello ile Merhaba kullanmaya **PUT** aşağıdaki hello yöntemiyle istek URI.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Merhaba istek URI'Sİ'da, şu parametreler hello değiştirin:

* **Abonelik kimliği:** Azure abonelik kimliğinizi  
* **Bulut hizmet adı:** hello bulut hizmeti toowhich hello isteği hello adını gönderilmeyecek.  
* **Otomasyon hesabı adı:** bulut hizmeti belirtilen hello içinde barındırılan automation hesabınız hello adı.  
* **İş Kimliği:** hello işi için GUID hello. PowerShell'de GUID'ler hello kullanarak oluşturulabilir **[GUID]::NewGuid(). ToString()** komutu.

Sipariş toopass parametreleri toohello runbook işi içinde hello istek gövdesi kullanın. Aşağıdaki JSON biçiminde sağlanan iki özelliklere hello alır:

* **Runbook adı:** gerekli. Merhaba iş toostart hello runbook adı Hello.  
* **Runbook parametreleri:** isteğe bağlı. Hello parametre listesi (adı, değer) sözlüğü biçiminde burada adı dize türünde olmalıdır ve değer geçerli bir JSON değeri olabilir.

Toostart hello istiyorsanız **Get-AzureVMTextual** daha önce oluşturulmuş runbook **VMName** ve **resourceGroupName** hello JSON biçimi aşağıdaki parametreleri olarak kullanma Merhaba istek gövdesi.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Merhaba işi başarıyla oluşturulduysa 201 HTTP durum kodu döndürülür. Yanıt Üstbilgileri ve hello yanıt gövdesi ile ilgili daha fazla bilgi için ilgili toohello makale çok başvurun[hello REST API kullanarak bir runbook işi oluşturun.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Bir runbook'u test ve parametreleri atayın
Olduğunda, [runbook'unuzu test hello taslak sürümünü](automation-testing-runbook.md) hello test seçeneğini kullanarak hello **Test** dikey penceresi açılır ve yeni oluşturduğunuz hello parametreleri için değerleri yapılandırabilirsiniz.

![Test ve ata parametreleri](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Bir zamanlama tooa runbook bağlamak ve parametreleri atayın
Yapabilecekleriniz [bir zamanlama Bağla](automation-schedules.md) tooyour runbook için belirli bir süre boyunca bu hello runbook başlatır. Giriş parametreleri hello zamanlama oluştururken ve hello zamanlamaya uygun olarak başlatıldı hello runbook bu değerleri için kullanacağı atayın. Tüm zorunlu parametre değerleri sağlanana kadar hello zamanlaması kaydedilemiyor.

![Zamanlama ve parametreleri atama](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Bir runbook için bir Web kancası oluşturun ve parametreleri atayın
Oluşturabileceğiniz bir [Web kancası](automation-webhooks.md) runbook'unuzu için ve runbook giriş parametreleri yapılandırın. Tüm zorunlu parametre değerleri sağlanana kadar hello Web kancası kaydedilemiyor.

![Web kancası oluşturun ve parametreleri atayın](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Bir Web kancası kullanarak bir runbook'u yürüttüğünüzde hello giriş parametresi önceden tanımlanmış  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  tanımladığınız hello giriş parametreleri birlikte gönderilir. Tooexpand hello tıklayabilirsiniz **WebhookData** daha fazla ayrıntı için parametre.

![WebhookData parametresi](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Sonraki adımlar
* Runbook giriş ve çıkış hakkında daha fazla bilgi için bkz: [Azure Automation: runbook giriş, çıkış ve iç içe runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).
* Farklı şekillerde toostart bir runbook hakkında daha fazla ayrıntı için bkz: [runbook başlatma](automation-starting-a-runbook.md).
* tooedit metin biçiminde runbook başvurmak çok[metinsel runbook'ları düzenleme](automation-edit-textual-runbook.md).
* tooedit grafik runbook başvurmak çok[Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).

