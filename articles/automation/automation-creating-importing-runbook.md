---
title: "aaaCreating veya bir Azure Otomasyonu runbook'u içeri aktarma"
description: "Bu makalede nasıl toocreate bir dosyadan içe veya Azure Otomasyonu yeni bir runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma
Otomasyon tarafından ya da bir runbook tooAzure ekleyebilirsiniz [yenisini oluşturmadan](#creating-a-new-runbook) veya mevcut bir runbook'u dosyadan veya hello alarak [Runbook Galerisi](automation-runbook-gallery.md). Bu makalede, oluşturma ve runbook'ları bir dosyadan içeri aktarma hakkında bilgiler sağlar.  Tüm topluluk runbook'ları ve modülleri erişme hello Ayrıntılar elde edebilirsiniz [Azure Otomasyonu Runbook ve modül galerileri](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Yeni bir runbook oluşturma
Azure Otomasyon hello Azure birini kullanarak yeni bir runbook oluşturabilirsiniz portalı veya Windows PowerShell. Merhaba runbook oluşturulduktan sonra bu bilgileri kullanarak düzenleyebilirsiniz [öğrenme PowerShell iş akışı](automation-powershell-workflow.md) ve [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalı ile yeni bir Azure Otomasyonu runbook
Yalnızca çalışabilirsiniz [PowerShell iş akışı runbook'ları](automation-runbook-types.md#powershell-workflow-runbooks) hello Azure Portalı'nda.

1. Hello Azure Klasik portalında tıklayın, **yeni**, **uygulama hizmetleri**, **Otomasyon**, **Runbook**, **Hızlıoluştur**.
2. Merhaba gerekli bilgileri girin ve ardından **oluşturma**. Merhaba runbook adı bir harf ile başlamalı ve harf, rakam, alt çizgi ve çizgi olabilir.
3. Tooedit hello runbook şimdi istiyorsanız, i **Runbook'u Düzenle**. Aksi takdirde tıklatın **Tamam**.
4. Yeni runbook'unuz hello üzerinde görünür **Runbook'lar** sekmesi.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate hello Azure portalı ile yeni bir Azure Otomasyonu runbook
1. Hello Azure portal, Automation hesabınızı açın.
2. Hub Hello seçin **Runbook'lar** tooopen hello listesini.
3. Tıklatın hello üzerinde **runbook Ekle** düğmesine ve ardından **yeni bir runbook oluşturmak**.
4. Tür a **adı** hello runbook ve select için kendi [türü](automation-runbook-types.md). Merhaba runbook adı bir harf ile başlamalı ve harf, rakam, alt çizgi ve çizgi olabilir.
5. Tıklatın **oluşturma** toocreate hello runbook ve açık hello Düzenleyici.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>Windows PowerShell ile yeni bir Azure Otomasyonu runbook toocreate
Merhaba kullanabilirsiniz [yeni AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate boş bir [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks). Merhaba ya da belirtebilirsiniz **adı** parametresi toocreate daha sonra düzenleyebilirsiniz veya hello belirtebilirsiniz boş bir runbook **yolu** parametresi tooimport runbook dosyası. Merhaba **türü** parametresi dahil toospecify hello dört runbook türlerden biri olmalıdır.

Merhaba aşağıdaki örnek komutlar Göster nasıl toocreate yeni bir boş runbook.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Bir runbook, Azure Automation'a bir dosyadan içeri aktarma
Azure Otomasyonu'nda bir PowerShell komut dosyası veya PowerShell iş akışı (.ps1 uzantılı) veya dışarı aktarılan bir grafik runbook (.graphrunbook) içeri aktararak, yeni bir runbook oluşturabilirsiniz.  Merhaba belirtmelisiniz [runbook türü](automation-runbook-types.md) hello alma hakkında önemli noktalar aşağıdaki hesap hello alma gelen oluşturulur.

* .Graphrunbook dosya yalnızca yeni bir alınabilir [grafik runbook](automation-runbook-types.md#graphical-runbooks), ve grafik runbook'lar .graphrunbook dosyasından yalnızca oluşturulabilir.
* Bir PowerShell iş akışı içeren bir .ps1 dosyası yalnızca içine aktarılabilen bir [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks).  Birden çok PowerShell iş akışı Hello dosya içeriyorsa, hello içeri aktarma başarısız olur. Her iş akışı tooits kendi dosyayı kaydedin ve her ayrı ayrı alın.
* Bir iş akışı içermeyen bir .ps1 dosyası da aktarılabilen bir [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) veya [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks).  İçine alınırsa bir PowerShell iş akışı runbook, ardından dönüştürülen tooa iş akışı olacaktır ve açıklamaları yapılan hello değişiklikler belirtme hello runbook'ta eklenecektir.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport bir dosyadan hello Klasik Azure portalı ile runbook
Azure Automation'a yordamı tooimport bir betik dosyasının aşağıdaki hello kullanabilirsiniz.  Bu portalı kullanarak bir PowerShell iş akışı runbook'u yalnızca bir .ps1 dosyasına aktarabilirsiniz unutmayın.  Diğer türleri için hello Azure portalını kullanmanız gerekir.

1. Hello Azure Yönetim Portalı'nda seçin **Otomasyon** ve ardından bir Otomasyon hesabı seçin.
2. **İçeri Aktar**’a tıklayın.
3. Tıklatın **dosyasına göz atın** ve hello komut dosyası tooimport bulun.
4. Tooedit hello runbook şimdi istiyorsanız, i **Runbook'u Düzenle**. Aksi takdirde, Tamam'ı tıklatın.
5. Merhaba yeni runbook hello üzerinde görünür **Runbook'lar** hello Otomasyon hesabı sekmesi.
6. Yapmanız gerekenler [yayımlama hello runbook](#publishing-a-runbook) çalıştırabilmeniz için önce.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport hello Azure portal ile bir dosyadan bir runbook
Azure Automation'a yordamı tooimport bir betik dosyasının aşağıdaki hello kullanabilirsiniz.  

> [!NOTE]
> Merhaba portalı kullanarak bir PowerShell iş akışı runbook'a yalnızca bir .ps1 dosyasına aktarabilirsiniz unutmayın.
> 
> 

1. Hello Azure portal, Automation hesabınızı açın.
2. Hub Hello seçin **Runbook'lar** tooopen hello listesini.
3. Tıklatın hello üzerinde **runbook Ekle** düğmesine ve ardından **alma**.
4. Tıklatın **Runbook dosyası** tooselect hello dosya tooimport
5. Merhaba, **adı** alan etkin sonra hello seçeneği toochange sahip.  Merhaba runbook adı bir harf ile başlamalı ve harf, rakam, alt çizgi ve çizgi olabilir.
6. Merhaba [runbook türü](automation-runbook-types.md) otomatik olarak seçilir, ancak hello geçerli kısıtlamaları göz önüne alındıktan sonra hello türünü değiştirebilirsiniz. 
7. Merhaba yeni runbook hello Otomasyon hesabı için runbook'ları hello listesinde görünür.
8. Yapmanız gerekenler [yayımlama hello runbook](#publishing-a-runbook) çalıştırabilmeniz için önce.

> [!NOTE]
> Bir grafik runbook veya bir grafik PowerShell iş akışı runbook içeri aktardıktan sonra hello seçeneği tooconvert toohello diğer türü istediyseniz sahip. Tootextual dönüştürülemiyor.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>Windows PowerShell ile bir betik dosyasından bir runbook'u tooimport
Merhaba kullanabilirsiniz [alma AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport PowerShell iş akışı runbook taslağı olarak bir komut dosyası. Merhaba runbook'un zaten olup olmadığını hello kullanmadığınız sürece hello içeri aktarma başarısız olur *-Force* parametresi. 

Aşağıdaki örnek komutlar hello nasıl tooimport bir komut dosyası bir runbook'a gösterir.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Runbook yayımlama
Oluşturduğunuzda ya da yeni bir runbook'u içeri çalıştırabilmeniz için önce onu yayımlamanız gerekir.  Otomasyon içindeki her runbook'un bir taslak ve bir yayımlanmış sürümü vardır. Yalnızca hello yayımlanan sürüm kullanılabilir toobe çalıştırmak ve yalnızca hello taslak sürüm düzenlenebilir. Merhaba yayımlanan sürüm herhangi bir değişiklik toohello Taslak sürümü tarafından etkilenmez. Merhaba Taslak sürümü kullanılabilir hale getirmek istediğinizde, daha sonra hangi hello yayımlanan sürüm hello taslak sürümle değiştirebilirsiniz yayımlayın.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>runbook hello Azure Klasik portalı kullanarak bir toopublish
1. Merhaba runbook hello Klasik Azure Portalı'nda açın.
2. Merhaba ekranında Hello üstünde tıklatın **Yazar**.
3. Merhaba ekranında Hello altındaki tıklatın **Yayımla** ve ardından **Evet** toohello doğrulama ileti.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>hello Azure portal kullanarak runbook'un bir toopublish
1. Merhaba runbook hello Azure portalını açın.
2. Merhaba tıklatın **Düzenle** düğmesi.
3. Merhaba tıklatın **Yayımla** düğmesine ve ardından **Evet** toohello doğrulama ileti.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>Windows PowerShell kullanarak bir runbook'un toopublish
Merhaba kullanabilirsiniz [Yayımla AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish bir runbook'u Windows PowerShell ile. Merhaba aşağıdaki örnek komutlar Göster nasıl toopublish bir örnek runbook.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Sonraki Adımlar
* toolearn nasıl hello Runbook ve PowerShell modülü Galerisi yararlanabilir hakkında bkz [Azure Otomasyonu Runbook ve modül galerileri](automation-runbook-gallery.md)
* bir metin düzenleyicisiyle PowerShell ve PowerShell iş akışı runbook'ları düzenleme hakkında daha fazla toolearn bakın [Azure Otomasyonu'nda metinsel runbook'lar düzenleme](automation-edit-textual-runbook.md)
* Grafik runbook yazma, hakkında daha fazla toolearn bakın [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md)

