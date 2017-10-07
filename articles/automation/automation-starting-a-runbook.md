---
title: Azure Automation runbook aaaStarting | Microsoft Docs
description: "Kullanılan toostart Azure Automation runbook olabilir ve her ikisi de kullanımıyla ilgili ayrıntılar Azure portalı ve Windows PowerShell hello sağlayan hello farklı yöntemler özetler."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Azure Otomasyonu runbook başlatma
Aşağıdaki tablonun hello hello yöntemi toostart en uygun tooyour belirli senaryo Azure Automation runbook belirlemenize yardımcı olur. Bu makalede Windows PowerShell ile hello Azure portal ile bir runbook'u başlatma hakkında bilgi içerir. Ayrıntılar üzerinde hello bağlantılar hello aşağıdaki erişebilirsiniz diğer belgelerinde diğer yöntemleri sağlanır.

| **YÖNTEMİ** | **ÖZELLİKLERİ** |
| --- | --- |
| [Azure Portal](#starting-a-runbook-with-the-azure-portal) |<li>En basit yöntem etkileşimli kullanıcı arabirimi ile.<br> <li>Form tooprovide basit parametre değerleri.<br> <li>İş durumu kolayca izleyin.<br> <li>İle Azure oturum açma kimliği doğrulanmış erişim. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Komut satırından Windows PowerShell cmdlet'leri ile çağırın.<br> <li>Birden çok adımı otomatik Çözümle eklenebilir.<br> <li>Sertifika veya OAuth kullanıcı asıl / hizmet isteği kimliği doğrulanır asıl.<br> <li>Basit ve karmaşık parametre değerlerini sağlayın.<br> <li>İş durumu izleyin.<br> <li>İstemci toosupport PowerShell cmdlet'leri gereklidir. |
| [Azure Otomasyonu API](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>En esnek yöntem, ancak ayrıca en karmaşık.<br> <li>HTTP isteği yapabilen dilediğiniz özel kodu çağırın.<br> <li>İstek sertifika ya da Oauth kullanıcı asıl / hizmet kimliği doğrulanmış sorumlu.<br> <li>Basit ve karmaşık parametre değerlerini sağlayın.<br> <li>İş durumu izleyin. |
| [Web kancaları](automation-webhooks.md) |<li>Runbook tek HTTP isteğinden başlatın.<br> <li>Güvenlik belirteci URL ile kimlik doğrulaması.<br> <li>İstemci Web kancası oluşturduğunuzda belirtilen parametre değerleri geçersiz kılamaz. Runbook hello HTTP istek ayrıntıları ile doldurulur tek bir parametre tanımlayabilirsiniz.<br> <li>Web kancası URL'si aracılığıyla özelliği hiçbir tootrack iş durumu. |
| [Yanıt tooAzure uyarı](../log-analytics/log-analytics-alerts.md) |<li>Bir runbook yanıt tooAzure uyarıda başlatın.<br> <li>Web kancası runbook için yapılandırmak ve tooalert bağlayın.<br> <li>Güvenlik belirteci URL ile kimlik doğrulaması. |
| [Zamanlama](automation-schedules.md) |<li>Saatlik, günlük, haftalık veya aylık zamanlamaya göre otomatik olarak runbook başlatın.<br> <li>Azure portal, PowerShell cmdlet'leri veya Azure API aracılığıyla zamanlama yönetme.<br> <li>Zamanlama ile kullanılan parametre değerleri toobe sağlar. |
| [Başka bir Runbook'tan](automation-child-runbooks.md) |<li>Bir runbook başka bir runbook'taki bir etkinlik olarak kullanın.<br> <li>Birden çok runbook tarafından kullanılan işlevselliği için kullanışlıdır.<br> <li>Parametre değerleri toochild runbook sağlayın ve çıktı üst runbook'ta kullanın. |

Merhaba aşağıdaki görüntüde ayrıntılı adım adım işlemi bir runbook'un hello yaşam döngüsü gösterilmektedir. Azure Automation'da bir runbook'u başlatan farklı yollar karma Runbook çalışanı tooexecute Azure Otomasyonu runbook'ları ve farklı bileşenler arasındaki etkileşimler için gerekli bileşenleri içerir. Otomasyon runbook'ları, veri merkezinizde, yürütülen toolearn başvurmak çok[karma runbook çalışanları](automation-hybrid-runbook-worker.md)

![Runbook mimarisi](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Hello Azure portal ile bir runbook başlatılıyor
1. Hello Azure portal, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını tıklatın.
2. Merhaba Hub menüsünde seçin **Runbook'lar**.
3. Merhaba üzerinde **Runbook'lar** dikey penceresinde, bir runbook seçin ve ardından **Başlat**.
4. Merhaba runbook'un parametreleri varsa, istendiğinde tooprovide değerler her parametre için bir metin kutusu olacaktır. Bkz: [Runbook parametreleri](#Runbook-parameters) altında daha fazla ayrıntı için parametreleri.
5. Merhaba üzerinde **iş** dikey penceresinde hello hello runbook işinin durumunu görüntüleyebilirsiniz.

## <a name="starting-a-runbook-with-windows-powershell"></a>Windows PowerShell ile bir runbook başlatılıyor
Merhaba kullanabilirsiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart bir runbook'u Windows PowerShell ile. Merhaba aşağıdaki örnek kod Test-Runbook adlı bir runbook başlatır.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

İşi Başlat AzureRmAutomationRunbook döndürür hello runbook başlatıldıktan sonra tootrack durumunu kullanabileceğiniz nesne. Bu iş nesnesi ile sonra kullanabileceğiniz [Get-AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) toodetermine hello hello işinin durumunu ve [Get-AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget çıktısını. Aşağıdaki örnek kod hello Test-Runbook, tamamlandı ve ardından çıktısını görüntüler tamamlanmasını bekler adlı bir runbook başlatır.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Merhaba runbook parametreleri gerektirir sonra bunları olarak sağlamalısınız bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) hello hashtable hello anahtarı hello parametre ve hello değerle eşleştiği hello parametre değeridir. Merhaba aşağıdaki örnek FirstName ve LastName, RepeatCount adlı bir tamsayı ve Show adlı bir boolean parametresiyle toostart iki dize parametresi ile bir runbook nasıl adlı gösterir. Parametreleri hakkında ek bilgi için bkz: [Runbook parametreleri](#Runbook-parameters) aşağıda.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Runbook parametreleri
Hello Azure Portal ya da Windows PowerShell bir runbook'u başlattığınızda hello yönerge hello Azure Otomasyonu web hizmeti gönderilir. Bu hizmet, karmaşık veri türleriyle parametreleri desteklemiyor. Karmaşık bir parametre için bir değer tooprovide ihtiyacınız varsa, satır içi başka bir runbook'tan açıklandığı gibi çağırmanız gerekir [alt runbook'ları Azure Automation](automation-child-runbooks.md).

Hello Azure Otomasyonu web hizmeti hello aşağıdaki bölümlerde açıklandığı gibi belirli veri türlerini kullanarak parametreler için özel işlevler sağlar.

### <a name="named-values"></a>Adlandırılmış değerler
Merhaba parametredir [object] veri türünü sonra onu listesini adlı değerleri JSON biçimi toosend aşağıdaki hello kullanabilirsiniz: *{Ad1: 'Değer1', ad2: 'Değer2', AD3: 'Değer3'}*. Bu değerler basit türler olmalıdır. Merhaba runbook hello parametre olarak alacağı bir [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) adlı değer tooeach karşılık gelen özelliklere sahip.

Kullanıcı adında bir parametre kabul eden test runbook aşağıdaki hello göz önünde bulundurun.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Merhaba aşağıdaki metni hello kullanıcı parametresi için kullanılabilir.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Çıktı aşağıdaki hello sonuçlanır.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Diziler
Merhaba parametresi [array] gibi bir dizi olup olmadığını veya [string []] kullanabileceğiniz sonra hello JSON biçimi toosend bu değerleri listesi: *[Value1, Value2, Value3]*. Bu değerler basit türler olmalıdır.

Adlı bir parametre kabul eden test runbook aşağıdaki hello göz önünde bulundurun *kullanıcı*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Merhaba aşağıdaki metni hello kullanıcı parametresi için kullanılabilir.

```
["Joe","Smith",2,true]
```

Çıktı aşağıdaki hello sonuçlanır.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Kimlik Bilgileri
Merhaba parametre veri türü ise **PSCredential**, bir Azure Otomasyonu hello adını sağlayın ve sonra [kimlik bilgisi varlığı](automation-credentials.md). Merhaba runbook belirttiğiniz hello ada sahip hello kimlik bilgisi alır.

Kimlik bilgisi adlı bir parametre kabul eden test runbook aşağıdaki hello göz önünde bulundurun.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Merhaba aşağıdaki metni adlı bir kimlik bilgisi varlığı olduğunu varsayarak hello kullanıcı parametresi için kullanılabilecek *My kimlik bilgisi*.

```
My Credential
```

Merhaba kimlik bilgisi Hello kullanıcı olduğu varsayılarak *jsmith*, bu çıkış aşağıdaki hello sonuçlanır.

```
jsmith
```

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba runbook mimari geçerli makalede kaynakları yöneten runbook Azure ve şirket içi hello karma Runbook çalışanı ile üst düzey bir genel bakış sağlar.  Otomasyon runbook'ları, veri merkezinizde, yürütülen toolearn başvurmak çok[karma Runbook çalışanları](automation-hybrid-runbook-worker.md).
* hakkında daha fazla özel veya ortak işlevleri için diğer runbook'lar tarafından kullanılan modüler runbook'lar toobe oluşturma hello toolearn başvurmak çok[alt runbook'ları](automation-child-runbooks.md).

