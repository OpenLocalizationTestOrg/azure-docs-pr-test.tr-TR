---
title: Azure Otomasyonu'nda aaaEditing metinsel runbook'lar
description: "Bu makalede farklı yordamlar PowerShell ve PowerShell iş akışı runbook'ları Azure Automation ile çalışmak için hello metin düzenleyicisini kullanarak sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Azure Otomasyonu metinsel runbook'larda düzenleme
Hello Azure Otomasyonu metin düzenleyicide kullanılan tooedit olabilir [PowerShell runbook'ları](automation-runbook-types.md#powershell-runbooks) ve [PowerShell iş akışı runbook'ları](automation-runbook-types.md#powershell-workflow-runbooks). IntelliSense ve ek özel özellikler tooassist ile kaynakları ortak toorunbooks erişirken kodlama renk gibi diğer kod Düzenleyicileri'nin hello tipik özellikler vardır.  Bu makalede, bu düzenleyicisiyle farklı işlevleri gerçekleştirmek için ayrıntılı adımlar sağlanmaktadır.

Merhaba metin düzenleyicisini runbook'a etkinlikler, varlıklar ve alt runbook'ları için bir özellik tooinsert kodu içerir. Merhaba kodu kendiniz yazmak yerine, kullanılabilir kaynaklar listesinden seçin ve hello runbook'a hello uygun kodu.

Azure Otomasyonu içindeki her runbook'un taslak ve yayımlanan olmak üzere iki sürümü vardır. Merhaba runbook'un taslak sürümünü hello düzenler ve yürütülmek üzere yayımlarsınız. Merhaba yayımlanan sürüm düzenlenemez. Bkz: [runbook yayımlama](automation-creating-importing-runbook.md#publishing-a-runbook) daha fazla bilgi için.

ile toowork [grafik Runbook'lar](automation-runbook-types.md#graphical-runbooks), bkz: [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit hello Azure portalı ile runbook
Aşağıdaki yordam tooopen hello metin düzenleyicide düzenlemek için bir runbook hello kullanın.

1. Hello Azure portal, Otomasyon hesabınızı seçin.
2. Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.
3. Merhaba adına tıklayın hello runbook'un tooedit istediğiniz ve hello ardından **Düzenle** düğmesi.
4. Düzenleme gerekli hello gerçekleştirin.
5. Tıklatın **kaydetmek** düzenlemeleriniz olduğunda tamamlandı.
6. Tıklatın **Yayımla** hello en son taslak sürümünün yayımlanan hello runbook toobe istiyorsanız.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>runbook'a bir cmdlet tooinsert
1. Hello hello metin düzenleyicisini tuvale, hello imleci tooplace hello cmdlet istediğiniz yere getirin.
2. Merhaba genişletin **cmdlet'leri** hello kitaplığı denetimi düğümünde.
3. Merhaba modülü toouse hello cmdlet'in içeren genişletin.
4. Merhaba cmdlet tooinsert sağ tıklatın ve seçin **toocanvas eklemek**.  Merhaba cmdlet'ini birden fazla parametre kümesi varsa, hello varsayılan kümesine eklenir.  Merhaba cmdlet tooselect farklı bir parametre genişletebilirsiniz ayarlayın.
5. Merhaba kodu hello cmdlet'i için tüm parametrelerin listesi ile eklenir.
6. Köşeli ayraçlar <> gerekli parametreleri için tarafından hello veri türü yerine uygun değeri girin.  Gerekli olmayan tüm parametreleri kaldırın.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>runbook'a bir alt runbook için tooinsert kodu
1. Hello hello metin düzenleyicisini tuvale, hello imleci tooplace hello kod Merhaba istediğiniz yere [alt runbook](automation-child-runbooks.md).
2. Merhaba genişletin **Runbook'lar** hello kitaplığı denetimi düğümünde.
3. Merhaba runbook tooinsert sağ tıklatın ve seçin **toocanvas eklemek**.
4. Merhaba kodu hello alt runbook için runbook parametreleri için herhangi bir yer tutucu ile eklenir.
5. Merhaba yer tutucuları, her parametre için uygun değerlerle değiştirin.

### <a name="tooinsert-an-asset-into-a-runbook"></a>bir runbook bir varlığa tooinsert
1. Hello hello metin düzenleyicisini tuvale, hello imleci hello alt runbook için tooplace hello kod istediğiniz yere getirin.
2. Merhaba genişletin **varlıklar** hello kitaplığı denetimi düğümünde.
3. Merhaba istediğiniz varlık türünü Hello düğümünü genişletin.
4. Merhaba varlık tooinsert sağ tıklatın ve seçin **toocanvas eklemek**.  İçin [değişken varlıkları](automation-variables.md), şunlardan birini seçin **"Değişken Al" toocanvas ekleme** veya **"Değişkenini Ayarla" toocanvas ekleme** tooget istediğiniz mı hello değişkenini bağlı olarak.
5. Merhaba kodu hello varlık için hello runbook'a eklenir.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit hello Azure portalı ile runbook
Aşağıdaki yordam tooopen hello metin düzenleyicide düzenlemek için bir runbook hello kullanın.

1. Hello Azure portal, seçin **Otomasyon** ve ardından bir Otomasyon hesabı hello adını tıklatın.
2. Select hello **Runbook'lar** sekmesi.
3. Merhaba adına tıklayın hello runbook'un tooedit istediğiniz ve hello ardından **Yazar** sekmesi.
4. Merhaba tıklatın **Düzenle** hello ekranın hello düğmesini.
5. Düzenleme gerekli hello gerçekleştirin.
6. Tıklatın **kaydetmek** düzenlemeleriniz olduğunda tamamlandı.
7. Tıklatın **Yayımla** hello en son taslak sürümünün yayımlanan hello runbook toobe istiyorsanız.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert runbook'a bir etkinlik
1. Hello hello metin düzenleyicisini tuvale, hello imleci tooplace hello etkinlik istediğiniz yere getirin.
2. Merhaba ekranında Hello altındaki tıklatın **Ekle** ve ardından **etkinlik**.
3. Merhaba, **tümleştirme Modülü** sütun, başlangıç etkinliği içeriyor select hello modülü.
4. Merhaba, **etkinlik** bölmesinde, bir etkinlik seçin.
5. Merhaba, **açıklama** sütun, Not hello hello etkinlik açıklaması. İsteğe bağlı olarak, ayrıntılı tıklayabilirsiniz toolaunch Yardım hello tarayıcıda hello etkinlik için Yardım.
6. Merhaba sağ oka tıklayın.  Hello etkinlik parametrelere sahipse, bunlar için bilgilerinizi listelenir.
7. Merhaba onay düğmesine tıklayın.  Kod toorun hello etkinlik hello runbook'a eklenir.
8. Merhaba etkinlik parametre gerektiriyorsa, köşeli ayraç <> tarafından hello veri türü yerine uygun değeri belirtin.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>runbook'a bir alt runbook için tooinsert kodu
1. Hello hello metin düzenleyicisini tuvale, hello imleci tooplace hello istediğiniz yere [alt runbook](automation-child-runbooks.md).
2. Merhaba ekranında Hello altındaki tıklatın **Ekle** ve ardından **Runbook**.
3. Merhaba runbook tooinsert hello Orta sütundan seçin ve hello sağ oka tıklayın.
4. Merhaba runbook'un parametreleri varsa bilgilendirme olarak listelenir.
5. Merhaba onay düğmesine tıklayın.  Kod toorun seçili hello runbook hello geçerli runbook'a eklenir.
6. Merhaba runbook parametre gerektiriyorsa, köşeli ayraç <> tarafından hello veri türü yerine uygun değeri belirtin.

### <a name="tooinsert-an-asset-into-a-runbook"></a>bir runbook bir varlığa tooinsert
1. Hello hello metin düzenleyicisini tuvale, hello imleci tooplace hello etkinlik tooretrieve hello varlık istediğiniz yere getirin.
2. Merhaba ekranında Hello altındaki tıklatın **Ekle** ve ardından **ayarı**.
3. Merhaba, **ayar eylemi** sütununda, istediğiniz select hello eylem.
4. Merhaba merkezi sütununda hello kullanılabilir varlıklar arasından seçim yapın.
5. Merhaba onay düğmesine tıklayın.  Tooget kod veya kümesi hello varlık hello runbook'a eklenmiş.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>Windows PowerShell kullanarak bir Azure Otomasyonu runbook'u tooedit
tooedit bir runbook'u Windows PowerShell ile Merhaba düzenleyiciyi kullanın ve tooa .ps1 dosyasına kaydedin. Merhaba kullanabilirsiniz [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) cmdlet tooretrieve hello hello runbook'un içeriğini ve ardından [kümesi AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello var Taslak runbook hello ile bir değiştirdi.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve hello bir Runbook'u Windows PowerShell kullanarak içeriği
Aşağıdaki örnek komutlar hello nasıl tooretrieve bir runbook betiğinin hello ve tooa komut dosyasını kaydedin gösterir. Bu örnekte, hello Taslak sürümü alınmaktadır. Bu sürüm değiştirilemez rağmen bu da olası tooretrieve hello yayımlanan hello runbook sürümüdür.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange hello bir Runbook'u Windows PowerShell kullanarak içeriği
Merhaba aşağıdaki örnek komutlar tooreplace hello bir runbook'un mevcut içeriğinin hello bir betik dosyasının içeriğiyle nasıl göstermektedir. Bu olduğu Merhaba, aynı Not Örnek yordamda olarak [tooimport Windows PowerShell ile bir betik dosyasından bir runbook'u](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>İlgili makaleler
* [Oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md)
* [PowerShell iş akışı öğrenme](automation-powershell-workflow.md)
* [Grafik Azure Otomasyonu'nda yazma](automation-graphical-authoring-intro.md)
* [Sertifikalar](automation-certificates.md)
* [Bağlantılar](automation-connections.md)
* [Kimlik Bilgileri](automation-credentials.md)
* [Zamanlamalar](automation-schedules.md)
* [Değişkenler](automation-variables.md)
