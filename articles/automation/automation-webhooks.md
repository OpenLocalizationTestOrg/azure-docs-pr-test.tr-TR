---
title: "bir Azure Otomasyonu runbook'u ile bir Web kancası aaaStarting | Microsoft Docs"
description: "Bir istemci toostart bir runbook'un Azure Otomasyonu'nda bir HTTP çağrısından veren bir Web kancası.  Bu makalede nasıl toocreate bir Web kancası ve nasıl toocall bir toostart bir runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Bir Web kancası ile bir Azure Otomasyonu runbook'u başlatma
A *Web kancası* toostart belirli bir runbook, Azure Otomasyonu'nda tek bir HTTP isteğini sağlar. Bu Visual Studio Team Services, GitHub, Microsoft Operations Management Suite günlük analizi veya özel uygulamalar gibi dış hizmetler toostart runbook'ları hello Azure Otomasyon API kullanarak tam bir çözüm uygulama olmadan sağlar.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

Bir runbook'u başlatma Web kancalarını tooother yöntemleri karşılaştırabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Bir Web kancası ayrıntıları
Merhaba aşağıdaki tabloda, bir Web kancası için yapılandırmanız gerekir hello özellikleri açıklar.

| Özellik | Açıklama |
|:--- |:--- |
| Ad |Bu yana bir Web kancası için istediğiniz herhangi bir ad toohello istemci gösterilmeyen sağlayabilir.  Yalnızca, tooidentify hello Azure automation'da runbook için kullanılır. <br>  Bir en iyi uygulama olarak kullanacağı bir ad ilgili toohello istemci hello Web kancası vermesi gerekir. |
| URL |Merhaba hello Web kancası hello benzersiz adresi bir istemci bir HTTP POST toostart hello runbook'la çağırır toohello Web kancası bağlı URL'sidir.  Merhaba Web kancası oluşturduğunuzda otomatik olarak oluşturulur.  Özel bir URL belirtemezsiniz. <br> <br>  Merhaba URL, başka kimlik doğrulama ile üçüncü taraf sistemleri tarafından çağrılan hello runbook toobe veren bir güvenlik belirteci içeriyor. Bu nedenle, bir parola gibi değerlendirilmelidir.  Güvenlik nedenleriyle, yalnızca hello hello zaman hello Web kancası Azure portalında URL'de oluşturulan görünüm hello olabilir. Gelecekte kullanım için güvenli bir konumda hello URL unutmamalısınız. |
| Sona erme tarihi |Bir sertifika gibi her Web kancası aynı zamanda bu artık kullanılabilir bir sona erme tarihi vardır.  Bu süre sonu tarihi Hello Web kancası oluşturulduktan sonra değiştirilebilir. |
| Etkin |Bir Web kancası oluşturulduğunda varsayılan olarak etkindir.  TooDisabled ayarlamak sonra hiçbir istemci mümkün toouse olacaktır.  Merhaba ayarlayabilirsiniz **etkin** hello Web kancası veya dilediğiniz zaman bir kez oluşturduğunuzda özelliği oluşturulur. |

### <a name="parameters"></a>Parametreler
Bir Web kancası hello runbook o Web kancası tarafından çalıştırıldığında kullanılan runbook parametreleri için değerleri tanımlayabilirsiniz. Merhaba Web kancası hello runbook'un zorunlu parametreler için değerler içermelidir ve isteğe bağlı parametreler için değerler içerebilir. Bir parametre değeri yapılandırılmış tooa Web kancası hello webhoook oluşturduktan sonra bile değiştirilebilir. Birden çok bağlantılı Web kancalarını tooa tek runbook her farklı parametre değerlerini kullanabilirsiniz.

Bir istemciyi bir Web kancası kullanarak bir runbook'u başlattığında, hello Web kancası içinde tanımlanan hello parametre değerleri geçersiz kılamaz.  tooreceive verileri hello istemcisinden hello runbook kabul edebileceği adlı tek bir parametre **$WebhookData** veri içeren türünü [object] hello istemci hello POST isteğinde içerir.

![Webhookdata özellikleri](media/automation-webhooks/webhook-data-properties.png)

Merhaba **$WebhookData** nesne hello aşağıdaki özelliklere sahiptir:

| Özellik | Açıklama |
|:--- |:--- |
| WebhookName |Merhaba Web kancası Hello adı. |
| RequestHeader |Hello gelen POST isteğinin Hello üstbilgiler içeren karma tablo. |
| RequestBody |Merhaba hello gelen POST isteğinin gövdesi.  Bu herhangi bir dize gibi JSON, XML, biçimlendirme korur veya kodlanmış form verileri. Merhaba runbook toowork beklenen hello veri biçimi ile yazılmış olmalıdır. |

Merhaba Web kancası gerekli toosupport Merhaba, yapılandırma yok **$WebhookData** parametresi ve hello runbook gerekli tooaccept değil.  Merhaba runbook hello parametre tanımlamıyorsa, ardından hello istemciden gönderilen hello isteğinin herhangi bir ayrıntıyı yoksayılır.

Merhaba Web kancası oluşturduğunuzda $WebhookData için bir değer belirtirseniz, hello Web kancası hello istemci POST isteğini hello verilerle hello runbook başlatıldığında hello istemci hello istek gövdesinde herhangi bir veri içermez olsa bile bu değer kılınmadı olacaktır.  Bir Web kancası dışında bir yöntem kullanılarak $WebhookData sahip bir runbook başlatırsanız, hello runbook tarafından tanınan $Webhookdata için bir değer sağlayabilir.  Bu değer hello sahip bir nesne olmalıdır aynı [özellikleri](#details-of-a-webhook) bir Web kancası tarafından geçirilen gerçek WebhookData çalıştığı gibi bu hello runbook düzgün çalışabilmesi için $Webhookdata olarak.

Runbook hello Azure Portalı ' aşağıdaki hello başlatma ve WebhookData bir nesne olduğundan, test etmek için bazı WebhookData örnek toopass istediğiniz, örneğin, bunu JSON olarak hello UI geçirilmesi gerekir.

![UI WebhookData parametresinden](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Aşağıdaki özelliklere hello WebhookData parametresi için hello varsa runbook yukarıda Hello için:

1. WebhookName: *MyWebhook*
2. RequestHeader: *= Test kullanıcıdan*
3. RequestBody: *["VM1", "VM2"]*

Ardından aşağıdaki JSON değeri hello UI hello WebhookData parametresi için de hello geçip geçmeyeceğini:  

* {"WebhookName": "MyWebhook", "RequestHeader": {"Kimden": "Test kullanıcı"}, "RequestBody": "[\"VM1\",\"VM2\"]"}

![Kullanıcı Arabirimi başlangıç WebhookData parametresi](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> Tüm giriş parametreleri Hello değerlerini hello runbook işi ile günlüğe kaydedilir.  Herhangi bir deyişle giriş hello Web kancası isteği hello istemci tarafından sağlanan erişim toohello Otomasyonu işi ile günlüğe kaydedilen ve kullanılabilir tooanyone olacaktır.  Bu nedenle, Web kancası çağrılarında hassas bilgiler dahil olmak üzere hakkında dikkatli olmanız gerekir.
>

## <a name="security"></a>Güvenlik
bir Web kancası Hello güvenliğini, çağrılan toobe veren bir güvenlik belirteci içeren URL'sini hello gizliliğini kullanır. Azure Otomasyonu toohello doğru URL'yi yapılan sürece hello isteği herhangi bir kimlik doğrulaması gerçekleştirmez. Bu nedenle, Web kancası hello isteği doğrulanırken bir alternatif şekillerini kullanmadan son derece hassas işlevleri gerçekleştirmek runbook'lar için kullanılmamalıdır.

Bunu hello denetleyerek bir Web kancası tarafından çağrıldı hello runbook toodetermine mantık içerebilir **WebhookName** hello $WebhookData parametresinin özelliği sağlar. Merhaba runbook gerçekleştirebilir daha fazla doğrulama hello belirli bilgileri arayarak **RequestHeader** veya **RequestBody** özellikleri.

Başka bir strateji toohave olup hello runbook bir Web kancası isteği alındığında bazı doğrulama dış bir koşulun gerçekleştirin.  Örneğin, yeni bir yürütme tooa GitHub havuz olduğunda GitHub tarafından çağrılan bir runbook'u göz önünde bulundurun.  Merhaba runbook yeni bir yürütme devam etmeden önce gerçekte yalnızca oluştu tooGitHub toovalidate bağlanabilir.

## <a name="creating-a-webhook"></a>Bir Web kancası oluşturma
Aşağıdaki yordam toocreate hello Azure portalında yeni bir Web kancası bağlı tooa runbook'ta hello kullanın.

1. Hello gelen **Runbook'lar dikey** hello Azure portal'ı tıklatın, ayrıntı dikey Web kancası hello hello runbook tooview başlayacak.
2. Tıklatın **Web kancası** hello dikey tooopen hello hello üstündeki **ekleme Web kancası** dikey. <br>
   ![Web kancası düğmesi](media/automation-webhooks/webhooks-button.png)
3. Tıklatın **yeni Web kancası oluşturma** tooopen hello **oluşturma Web kancası dikey**.
4. Belirtin bir **adı**, **sona erme tarihi** hello Web kancası ve olup etkinleştirilmelidir. Bkz: [bir Web kancası ayrıntılarını](#details-of-a-webhook) daha fazla bilgi için bu özellikleri.
5. Merhaba Kopyala simgesine tıklayın ve toocopy hello URL'sini hello Web kancası Ctrl + C tuşlarına basın.  Ardından güvenli bir yerde kaydedin.  **Merhaba Web kancası oluşturulduktan sonra hello URL yeniden alınamıyor.** <br>
   ![Web kancası URL'si](media/automation-webhooks/copy-webhook-url.png)
6. Tıklatın **parametreleri** hello runbook parametreleri için tooprovide değerleri.  Merhaba runbook zorunlu parametreler varsa, değerleri belirtilmediği sürece sonra mümkün toocreate hello Web kancası olmaz.
7. Tıklatın **oluşturma** toocreate hello Web kancası.

## <a name="using-a-webhook"></a>Bir Web kancası kullanma
toouse bir Web kancası oluşturulduktan sonra istemci uygulamanız bir HTTP POST hello Web kancası için hello URL'siyle kesmeniz gerekir.  Merhaba Web kancası Hello sözdizimi biçimini izleyen hello olacaktır.

    http://<Webhook Server>/token?=<Token Value>

Merhaba istemci hello POST isteğinden dönüş kodları aşağıdaki hello birini alır.  

| Kod | Metin | Açıklama |
|:--- |:--- |:--- |
| 202 |Kabul edildi |Merhaba istek kabul edildi ve hello runbook başarıyla sıraya alındı. |
| 400 |Hatalı istek |Merhaba isteği hello aşağıdaki nedenlerden birinden dolayı kabul edilmedi. <ul> <li>Merhaba Web kancası süresi doldu.</li> <li>Merhaba Web kancası devre dışı bırakılır.</li> <li>Merhaba URL'de Hello belirteci geçersiz.</li>  </ul> |
| 404 |Bulunamadı |Merhaba isteği hello aşağıdaki nedenlerden birinden dolayı kabul edilmedi. <ul> <li>Merhaba Web kancası bulunamadı.</li> <li>Merhaba runbook bulunamadı.</li> <li>Merhaba hesabı bulunamadı.</li>  </ul> |
| 500 |İç sunucu hatası |Merhaba URL geçerli, ancak bir hata oluştu.  Lütfen hello isteği yeniden gönderin. |

Merhaba istek başarılı olduğunu varsayarak, hello Web kancası yanıt gibi JSON biçiminde hello iş kimliği içerir. Tek iş kimliği yer alır ancak hello JSON biçimi için gelecekteki olası geliştirmeleri sağlar.

    {"JobIds":["<JobId>"]}  

Merhaba istemci hello runbook işi tamamlandığında veya hello Web kancası gelen tamamlanma durumu belirlenemiyor.  Merhaba iş kimliği gibi başka bir yöntemle kullanarak bu bilgileri belirleyebilirsiniz [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) veya hello [Azure Otomasyon API](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Örnek
Merhaba örnek aşağıdaki Windows PowerShell toostart bir runbook ile bir Web kancası kullanır.  Bir HTTP isteği yapabilen herhangi bir dil bir Web kancası kullanabileceğinizi unutmayın; Windows PowerShell yalnızca kullanılan burada bir örnek olarak.

Merhaba runbook hello hello istek gövdesinde JSON biçimli sanal makinelerin listesini bekliyor. Biz de hello hello istek üstbilgisinde başlatıldığına kimin hello runbook'u ve başlangıç tarihi ve saati başlatma hakkında bilgi dahil.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Merhaba aşağıdaki görüntüde hello üstbilgi bilgileri gösterir (kullanarak bir [Fiddler](http://www.telerik.com/fiddler) izleme) bu istek. Bu standart bir HTTP istek üstbilgilerinin toplama toohello içerir özel tarih ve eklediğimiz üstbilgileri.  Bu değerlerin her birini hello kullanılabilir toohello runbook'ta olan **RequestHeaders** özelliği **WebhookData**.

![Web kancası düğmesi](media/automation-webhooks/webhook-request-headers.png)

Merhaba aşağıdaki resimde gösterilmiştir hello hello istek gövdesi (kullanarak bir [Fiddler](http://www.telerik.com/fiddler) izleme) olan kullanılabilir toohello runbook'ta hello **RequestBody** özelliği **WebhookData**. Merhaba hello istek gövdesinde eklenmiştir hello biçimi olduğu için bu JSON olarak biçimlendirilir.     

![Web kancası düğmesi](media/automation-webhooks/webhook-request-body.png)

Merhaba aşağıdaki görüntüde Windows PowerShell ve hello elde edilen yanıt gönderilen hello istek gösterilir.  Merhaba iş kimliği hello yanıt ve dönüştürülen tooa dize ayıklanır.

![Web kancası düğmesi](media/automation-webhooks/webhook-request-response.png)

Merhaba aşağıdaki örnek runbook'u hello önceki örnek isteğini kabul eder ve hello sanal makineleri hello istek gövdesinde belirtilen başlatır.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>Başlangıç runbook'larda yanıt tooAzure uyarıları
Web kancası etkin runbook'ları olabilir kullanılan tooreact çok[Azure uyarıları](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Azure kaynaklarında performans, kullanılabilirlik ve kullanım hello Yardım Azure uyarıları gibi hello istatistikleri toplama tarafından izlenebilir. Ölçümleri izleme dayalı bir uyarı alabilirsiniz veya Azure kaynaklarınızı, şu anda Otomasyon hesapları için olaylar yalnızca ölçümleri destekler. Atanan hello eşiği veya yapılandırılmış hello olay tetiklenir sonra toohello Hizmet Yöneticisi veya ortak yöneticileri tooresolve hello uyarı ölçümleri hakkında daha fazla bilgi için bir bildirim gönderilir ve olayları başvurun çok belirtilen bir ölçüm hello değerini aştığında[ Azure uyarıları](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Azure Uyarıları Bildirim sistemi olarak kullanmanın yanı sıra, ayrıca yanıt tooalerts runbook'ları devre dışı tetiklersiniz. Azure Otomasyonu hello yetenek toorun Web kancası etkin runbook'ları Azure uyarılar sağlar. Ölçüm aştığında hello eşik değeri hello uyarı kuralı etkin hale gelir ve Tetikleyicileri hello runbook sırayla yürüten Otomasyonu Web kancası hello yapılandırılmış.

![Web kancaları](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Uyarı bağlamı
Bir sanal makine gibi bir Azure kaynağı düşünün, CPU kullanımı bu makinenin hello anahtar performans ölçüm biridir. Merhaba CPU kullanımı % 100 veya belirli bir miktar fazla uzun süre ise toorestart hello sanal makine toofix hello sorun isteyebilirsiniz. Bu bir uyarı kuralı toohello sanal makine yapılandırarak çözülebilir ve bu kural CPU yüzdesi, ölçüm olarak alır. CPU yüzdesi burada yalnızca bir örnek olarak alınır ancak tooyour Azure yapılandırabileceğiniz birçok ölçümleri vardır kaynakları ve hello sanal makinenin yeniden başlatılması olan bir eylemi toofix bu sorunu gerçekleştirilen diğer eylemler hello runbook tootake yapılandırabilirsiniz.

Bu hello uyarı kuralı etkin hale gelir ve Web kancası etkin runbook Tetikleyicileri hello zaman hello uyarı bağlamı toohello runbook gönderir. [Uyarı bağlamı](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) dahil olmak üzere ayrıntılarını içeren **Subscriptionıd**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** ve **zaman damgası** üzerinde bu göz önünde bulundurarak eylem hello runbook tooidentify hello kaynağı için gerekli olan. Bağlam içinde hello hello gövde bölümü katıştırılmış uyarı **WebhookData** gönderilen toohello runbook nesne ve ile erişilebilir **Webhook.RequestBody** özelliği

### <a name="example"></a>Örnek
Bir Azure sanal makinesi, abonelik ve ilişkilendirme oluşturma bir [uyarı toomonitor CPU yüzdesi ölçüm](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Merhaba uyarı oluşturulurken hello Web kancası oluşturulurken oluşturulan hello Web kancası hello URL'si ile Merhaba Web kancası alanını doldurmak emin olun.

Merhaba aşağıdaki örnek runbook'u hello uyarı kuralı etkin hale gelir ve hello runbook tooidentify hello kaynak üzerinde bu eylemi gerçekleştirmeden gereken hello uyarı bağlam parametreleri toplar geldiğinde tetiklenir.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Sonraki adımlar
* Farklı şekillerde toostart bir runbook hakkında daha fazla bilgi için bkz: [Runbook başlatma](automation-starting-a-runbook.md).
* Bir Runbook işinin durumunu görüntüleme hello hakkında daha fazla bilgi için çok başvuran[Azure Otomasyonu Runbook yürütme](automation-runbook-execution.md).
* nasıl toouse Azure Otomasyonu tootake eylem Azure uyarılar hakkında bkz toolearn [Otomasyon runbook'ları ile Azure VM uyarıları düzeltmek](automation-azure-vm-alert-integration.md).
