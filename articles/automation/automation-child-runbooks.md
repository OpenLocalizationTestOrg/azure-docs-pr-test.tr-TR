---
title: Azure Otomasyonu aaaChild runbook'larda | Microsoft Docs
description: "Azure Otomasyonu'nda başka bir runbook'tan runbook başlatma ve bunlar arasında bilgi paylaşımı için farklı yöntemler hello açıklar."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Azure Otomasyonu'nda alt runbook'lar
Bunu bir Azure Otomasyonu toowrite yeniden kullanılabilir, modüler runbook'lar diğer runbook'lar tarafından kullanılabilen ayrı işleve sahip en iyi uygulamadır. Üst runbook genellikle bir veya daha fazla alt runbook'lar gerekli tooperform işlevi çağırır. Bir alt runbook'u iki yolu toocall vardır ve her anlamanız gereken belirli farklara sahiptir, farklı senaryolarınız için en iyi olacağı belirleyebilmesi.

## <a name="invoking-a-child-runbook-using-inline-execution"></a>Satır içi yürütme kullanarak bir alt runbook çağırma
bir runbook'u satır içi tooinvoke başka bir runbook'tan hello runbook hello adını kullanın ve tam olarak, bir etkinlik veya cmdlet'i kullanırken yaptığınız gibi parametreleri için değerler sağlayın.  Tüm runbook'ları hello aynı Otomasyon hesabı kullanılabilir tooall diğerleri toobe bu yöntemle kullanılan alanlarıdır. Merhaba üst runbook toohello sonraki satıra geçmeden önce hello alt runbook toocomplete için bekler ve herhangi bir çıkış doğrudan toohello üst döndürülür.

Bir runbook'u satır içi çağırdığınızda hello aynı hello üst runbook işi çalıştırır. Çalıştırdığınız hello alt runbook'un hello iş geçmişinde hiçbir belirti olmaz. Tüm özel durumlar ve akış hello alt runbook'tan hello üst öğesi ile ilişkilendirilir. Bu daha az iş çalıştırılır ve bunları tootrack ve tootroubleshoot hello alt runbook tarafından karşılaşılan özel durumlar itibaren kolaylaştırır ve akış çıktısını hello üst işle ilişkili olan.

Bir runbook yayımlandığında, bu runbook'un çağırdığı tüm alt runbook zaten yayımlanması gerekir. Azure Otomasyonu runbook derlendiğinde alt runbook'larla bir ilişkilendirme derlemeler olmasıdır. Yoksa, hello üst runbook toopublish düzgün görünür ancak başlatıldığında bir özel durum oluşturur. Bu durumda, sipariş tooproperly başvuru hello alt runbook'hello üst runbook yeniden yayımlayabilirsiniz. Merhaba ilişki zaten oluşturulmuş olduğundan hello alt runbook'ları hiçbirini değiştirilirse toorepublish hello üst runbook gerekmez.

Satır içi olarak adlandırılan bir alt runbook'un Hello parametreleri karmaşık nesneler de dahil olmak üzere herhangi bir veri türü olabilir ve var. hiçbir [JSON serileştirmesi](automation-starting-a-runbook.md#runbook-parameters) hello Azure Yönetim Portalı kullanarak hello runbook'u başlattığınızda veya hello olduğundan Start-AzureRmAutomationRunbook cmdlet'ini kullanın.

### <a name="runbook-types"></a>Runbook türleri
Hangi tür birbirine çağırabilirsiniz:

* A [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) ve [grafik runbook'lar](automation-runbook-types.md#graphical-runbooks) (her ikisi de olan temel PowerShell) her bir satır çağırabilirsiniz.
* A [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks) ve grafik PowerShell iş akışı runbook'ları (her ikisi de olan temel PowerShell iş akışı) her bir satır çağırın
* PowerShell türleri hello ve PowerShell iş akışı türleri hello birbirine satır içi çağrılamıyor ve başlangıç AzureRmAutomationRunbook kullanmanız gerekir.

Zaman sipariş sağlasa da yayımlayın:

* Merhaba, PowerShell iş akışı ve grafik PowerShell iş akışı runbook için runbook'ları yalnızca önemlidir dizisi yayımlayın.

Satır içi yürütme kullanarak bir grafik veya PowerShell iş akışı alt runbook'u çağırdığınızda, yalnızca hello runbook hello adını kullanabilirsiniz.  PowerShell alt runbook çağırdığınızda, gerekir öncesinde adıyla *.\\*  betik hello toospecify hello yerel dizininde bulunur. 

### <a name="example"></a>Örnek
Aşağıdaki örnek hello üç parametre, karmaşık bir nesne, bir tamsayı ve bir Boole değeri kabul eden bir test alt runbook'u çağırır. Merhaba hello alt runbook'un çıktısını tooa değişkeni atanır.  Bu durumda, bir PowerShell iş akışı runbook hello alt runbook.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

Aşağıdadır hello hello alt öğesi olarak bir PowerShell runbook kullanarak aynı örneği.

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>Cmdlet'ini kullanarak bir alt runbook'u başlatma
Merhaba kullanabilirsiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) cmdlet toostart açıklandığı gibi bir runbook [toostart Windows PowerShell ile bir runbook](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell). Bu cmdlet kullanım iki modu mevcuttur.  Merhaba alt iş hello alt runbook için oluşturulan hemen bir modda hello cmdlet hello iş kimliği döndürür.  İçinde hello belirterek etkinleştirmek diğer modu hello **-bekleyin** parametresi hello cmdlet hello alt kadar bekler işi bittiğinde ve hello çıktı hello alt runbook'tan döndürür.

Merhaba iş bir alt runbook'tan bir cmdlet'le başlatılan hello üst runbook'tan ayrı bir iş çalıştırılır. Bu hello runbook'u satır içi çağırma'den daha fazla iş sonuçlanır ve daha zor tootrack yapar. Merhaba üst birden çok alt runbook için her toocomplete beklemeden zaman uyumsuz olarak başlatabilirsiniz. Merhaba alt runbook'ların satır içi olarak çağrıldığı Paralel yürütme türü için hello üst runbook toouse hello gerekir [parallel anahtar kelimesini](automation-powershell-workflow.md#parallel-processing).

Bir cmdlet'le başlatılan bir alt runbook'un parametreleri açıklandığı gibi karma tablosu olarak sağlanır [Runbook parametreleri](automation-starting-a-runbook.md#runbook-parameters). Yalnızca basit veri türleri kullanılabilir. Ardından Hello runbook karmaşık veri türüne sahip bir parametre varsa, satır içi çağrılmalıdır.

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek bir alt runbook parametreleri ve ardından bekler hello başlangıç AzureRmAutomationRunbook kullanarak toocomplete başlar-parametre bekleyin. Tamamlandığında, çıktısını hello alt runbook'tan toplanır.

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>Alt runbook çağırma yöntemlerinin karşılaştırılması
Merhaba aşağıdaki tabloda hello hello başka bir runbook'tan bir runbook'u çağırmak için iki yöntem arasındaki farklar özetlenmektedir.

|  | Satır içi | Cmdlet |
|:--- |:--- |:--- |
| İş |Alt runbook'ları hello aynı hello üst öğe olarak işi çalıştırın. |Merhaba alt runbook için ayrı bir iş oluşturulur. |
| Yürütme |Üst runbook devam etmeden önce hello alt runbook toocomplete için bekler. |Üst runbook alt runbook başlatıldıktan hemen sonra devam *veya* üst runbook hello alt iş toofinish için bekler. |
| Çıktı |Üst runbook doğrudan alt runbook'tan çıkış alabilir. |Üst runbook alt runbook işinden çıkış almak gerekir *veya* üst runbook alt runbook'tan çıkış doğrudan alabilirsiniz. |
| Parametreler |Merhaba alt runbook parametreleri için değerleri ayrı ayrı belirtilir ve herhangi bir veri türü kullanabilirsiniz. |Parametreleri tek bir karma tablosunda birleştirilmelidir ve yalnızca basit, içerebilir hello alt runbook için değerleri dizisi ve JSON serileştirmesi kullanan veri türleri nesne. |
| Otomasyon Hesabı |Üst runbook alt runbook hello kullanma yalnızca aynı automation hesabı. |Üst runbook alt runbook'tan herhangi bir Otomasyon hesabı hello gelen kullanabileceğiniz aynı Azure aboneliği ve bir bağlantı tooit varsa bile farklı bir abonelik. |
| Yayımlama |Üst runbook yayımlanmadan önce alt runbook yayımlanmalıdır. |Üst runbook başlatılmadan önce dilediğiniz zaman alt runbook yayımlanmalıdır. |

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md)
* [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)

