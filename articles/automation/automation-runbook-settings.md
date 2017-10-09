---
title: "aaaRunbook ayarları | Microsoft Docs"
description: "Azure Automation runbook Hello yapılandırma ayarlarını açıklar ve nasıl her ikisini de kullanarak bunları hello Azure Yönetim Portalı ve Windows PowerShell toochange."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Runbook ayarları
Azure Otomasyonu içindeki her runbook'un günlüğe kaydetme davranışını tanımlanan toobe ve toochange yardımcı birden çok ayara sahiptir. Bu ayarların her biri aşağıda hakkında yordamlar tarafından izlenen açıklanan toomodify bunları.

## <a name="settings"></a>Ayarlar
### <a name="name-and-description"></a>Ad ve açıklama
Oluşturulduktan sonra bir runbook hello adını değiştiremezsiniz. Merhaba Açıklama isteğe bağlıdır ve too512 karakter olabilir.

### <a name="tags"></a>Etiketler
Etiketler, tooassign ayrı sözcükleri ve tümcecikleri toohelp bir runbook'u tanımlamaya izin verir. Örneğin, ne zaman gönderdiğiniz bir runbook toohello [PowerShell Galerisi](https://www.powershellgallery.com/), belirli etiketleri tooidentify kategorilerini hello runbook listelenen belirtin. Bir runbook için birden çok etiket virgül ile ayırarak belirtebilirsiniz.

### <a name="logging"></a>Günlüğe kaydetme
Varsayılan olarak, ayrıntılı ve ilerleme durumu kayıtlarını toojob geçmişine yazılmaz. Bu kayıtları belirli runbook toolog hello ayarlarını değiştirebilirsiniz. Bu kayıtlar hakkında daha fazla bilgi için bkz: [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Runbook ayarlarını değiştirme

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Hello Azure portalı ile runbook ayarlarını değiştirme
Hello hello Azure Portalı'nda bir runbook ayarlarını değiştirebilirsiniz **ayarları** dikey penceresinde hello runbook için.

1. Hello Azure portal, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını tıklatın.
2. Select hello **Runbook'lar** sekmesi.
3. Bir runbook'un Hello adına tıklayın ve yönlendirilmiş toohello ayarları dikey penceresinde hello runbook. Buradan belirtin veya etiketleri değiştirebilir, runbook açıklaması Merhaba, günlüğe kaydetme ve izleme ayarlarını yapılandırın ve sorunları çözmek Destek Araçları toohelp erişim.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Windows PowerShell ile runbook ayarlarını değiştirme
Merhaba kullanabilirsiniz [kümesi AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) bir runbook için cmdlet toochange hello ayarları. Birden çok etiket toospecify istiyorsanız, virgülle ayrılmış değerler toohello etiketleri parametresi ile bir dizi veya tek bir dize ya da sağlayabilir. Merhaba geçerli hello etiketleriyle alabilirsiniz [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Aşağıdaki örnek komutlar hello tooset hello bir runbook'un özelliklerinin nasıl gösterir. Bu örnek toohello varolan etiketleri ve ayrıntılı kayıtları günlüğe kaydedileceğini belirtir üç etiketleri ekler.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Sonraki adımlar
* toocreate ve alma çıkış ve hata iletileri, runbook'lardan nasıl görürüm toolearn [Runbook çıkışı ve iletileri](automation-runbook-output-and-messages.md) 
* tooadd hello topluluk veya başka kaynak veya toocreate kendi runbook zaten geliştirilmiştir bir runbook nasıl görürüm toounderstand [oluşturma veya bir Runbook'u içeri aktarma](automation-creating-importing-runbook.md) 

