---
title: "JSON biçimli etiketler tooschedule Azure VM durumunu aaaUse | Microsoft Docs"
description: "Bu makalede etiketler tooautomate hello VM başlatma ve kapatma zamanlama üzerinde nasıl toouse JSON dizeler gösterilmektedir."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a>Azure otomasyonu senaryosu: kullanarak JSON biçimli etiketler toocreate Azure VM başlatma ve kapatma için bir zamanlama
Müşteriler genellikle tooschedule hello başlangıç istediğiniz ve sanal makineleri toohelp kapatma abonelik maliyetlerini azaltmak veya işletme ve teknik gereksinimleri destekler.

Merhaba aşağıdaki senaryoyu tooset otomatik başlatma ve kapatma, VM'lerin bir kaynak grubu düzeyinde veya azure'da sanal makine düzeyinde Schedule adlı bir etiket kullanarak sağlar. Bu zamanlamanın başlangıç zamanı ve kapatma süresi ile Pazar tooSaturday gelen yapılandırılabilir.

Biz, bazı Giden kutusu seçeneğiniz vardır. Bunlar:

* [Sanal makine ölçek kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooscale içeri veya dışarı etkinleştirmek otomatik ölçeklendirme ayarları.
* [DevTest Labs](../devtest-lab/devtest-lab-overview.md) hizmetini başlatma ve kapatma işlemleri planlama hello yerleşik özelliğine sahiptir.

Ancak, bu yalnızca belirli senaryolar destek seçenekleri ve uygulanan tooinfrastructure olarak-hizmet (Iaas) VM'ler olamaz.

Merhaba zamanlama etiketi uygulanan tooa kaynak grubu olduğunda, aynı zamanda uygulanan tooall sanal makineler bu kaynak grubu içinde olur. Bir zamanlama da doğrudan uygulanan tooa VM ise, hello son zamanlama sırasının hello önceliklidir:

1. Zamanlama uygulanan tooa kaynak grubu
2. Uygulanan tooa kaynak grubu ve hello kaynak grubundaki sanal makine zamanlama
3. Uygulanan tooa sanal makine zamanlama

Bu senaryo, aslında bir JSON dizesinde belirtilen biçiminde alır ve hello değeri olarak ekler Schedule adlı bir etiket için. Ardından bir runbook'un tüm kaynak grupları ve sanal makineleri listeler ve daha önce listelenen hello senaryolarını temel alarak her VM için hello zamanlamalar tanımlar. Sonraki bağlı zamanlamaları var. VM'ler hello döngüler ve ne yapılması değerlendirir. Örneğin, bunu VM'ler durduruldu, kapatmak veya göz ardı toobe gereken belirler.

Bu runbook'lar hello kullanarak kimlik doğrulaması [Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md).

## <a name="download-hello-runbooks-for-hello-scenario"></a>Merhaba runbook'lar hello senaryo için karşıdan yükle
Bu senaryo hello indirebilirsiniz dört PowerShell iş akışı runbook oluşur [TechNet Galerisi](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) veya hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) bu proje için depo.

| Runbook | Açıklama |
| --- | --- |
| Test-ResourceSchedule |Her sanal makine zamanlamayı denetler ve kapanması veya başlatılması hello zamanlamaya bağlı olarak gerçekleştirir. |
| Ekleme ResourceSchedule |VM veya kaynak Hello zamanlama etiketi tooa grubu ekler. |
| Güncelleştirme ResourceSchedule |Yeni bir tane ile değiştirerek Hello varolan bir zamanlamayı etiketi değiştirir. |
| Remove-ResourceSchedule |Merhaba zamanlama etiketi bir VM veya kaynak grubundan kaldırır. |

## <a name="install-and-configure-this-scenario"></a>Bu senaryoyu yükleme ve yapılandırma
### <a name="install-and-publish-hello-runbooks"></a>Yükleme ve yayımlama hello runbook'ları
Merhaba runbook'ları indirdikten sonra bunları hello yordamı kullanarak içeri aktarabilirsiniz [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).  Otomasyon hesabınızda başarıyla alındıktan sonra her runbook yayımlayın.

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a>Zamanlama toohello Test ResourceSchedule runbook Ekle
Merhaba Test ResourceSchedule runbook için bu adımları tooenable hello zamanlama izleyin. Kapalı hangi sanal makinelerin başlatılmalıdır doğrular hello runbook veya olarak sol budur.

1. Hello Azure portal, Automation hesabınızı açın ve hello ardından **Runbook'lar** döşeme.
2. Merhaba üzerinde **Test ResourceSchedule** dikey penceresinde hello tıklatın **zamanlamaları** döşeme.
3. Merhaba üzerinde **zamanlamaları** dikey penceresinde tıklatın **bir zamanlama Ekle**.
4. Merhaba üzerinde **zamanlamaları** dikey penceresinde, select **bir zamanlama tooyour runbook bağlantı**. Ardından **yeni bir zamanlama oluşturmak**.
5. Merhaba üzerinde **yeni zamanlama** dikey penceresinde hello ad yazın, bu zamanlamanın örneğin: *HourlyExecution*.
6. Merhaba zamanlama için **Başlat**, hello başlangıç zaman tooan saat artışı ayarlayın.
7. Seçin **yineleme**ve ardından **her aralığı yinelenmesini**seçin **1 saat**.
8. Doğrulayın **sona erme süresini ayarlamanıza** çok ayarlanır**Hayır**ve ardından **oluşturma** toosave yeni zamanlamanızı.
9. Merhaba üzerinde **zamanlama Runbook** seçenekleri dikey penceresinde, select **parametreler ve çalıştırma ayarları**. Merhaba Test ResourceSchedule içinde **parametreleri** dikey penceresinde hello aboneliğinizi hello adını girin **varlığıyla SubscriptionName** alan.  Merhaba runbook için gerekli olan tek bir parametre hello budur.  İşiniz bittiğinde tıklatın **Tamam**.

tamamlandığında hello runbook zamanlaması hello aşağıdaki gibi görünmelidir:

![Yapılandırılmış Test ResourceSchedule runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a>Biçim hello JSON dizesi
Bu çözüm, JSON ile belirtilen bir biçim dizesi ve bir etiket için başlangıç değeri olarak ekler alır zamanlama temel olarak çağrılır. Ardından bir runbook'un tüm kaynak grupları ve sanal makineleri listeler ve her bir sanal makine için hello zamanlamaları tanımlar.

Merhaba runbook hello sanal makineleri bağlı zamanlamaları var. döngüler ve hangi eylemleri alınıp alınmayacağını denetler. Merhaba, hello çözümleri nasıl biçimlendirilmiş bir örnek verilmiştir:

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

Bu yapı hakkında ayrıntılı bazı bilgiler aşağıdadır:

1. Merhaba bu JSON yapısındaki en iyi duruma getirilmiş toowork Azure içindeki bir tek etiket değeri hello 256 karakterlik yazıtiplerinden biçimidir.
2. *TZID* hello hello sanal makinenin saat dilimini temsil eder. Bu kodu bir PowerShell oturumu--içinde hello Timezoneınfo .NET sınıfını kullanarak elde edilebilir**[System.TimeZoneInfo]:: GetSystemTimeZones()**.

   ![PowerShell'de GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * Haftanın günü sıfır toosix sayısal bir değeri ile temsil edilir. Merhaba değeri sıfır Pazar eşittir.
   * Merhaba başlangıç saati hello ile temsil edilen **S** özniteliği ve değerini 24 saat biçiminde değil.
   * Merhaba son veya kapatma süresi hello ile temsil edilen **E** özniteliği ve değerini 24 saat biçiminde değil.

     Merhaba, **S** ve **E** her özniteliklere sahip bir değeri sıfır (0), hello sanal makine sol değerlendirme hello aynı anda mevcut durumda.
3. Merhaba haftanın belirli bir gün için tooskip değerlendirme istiyorsanız, o hello haftanın günü için bir bölüm eklemeyin. Merhaba örneği, yalnızca Pazartesi aşağıdaki değerlendirilir ve hello hello haftanın diğer günleri göz ardı edilir:

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a>Etiket kaynak grupları veya VM'ler
tooshut VM'ler aşağı tootag ihtiyacınız hello VM'ler veya hello kaynak grupları, bunlar bulunduğu. Bir zamanlama etiketi sahip olmayan sanal makineleri değerlendirilmez. Bu nedenle, bunlar çalışmaya veya kapat.

Bu çözüm ile iki şekilde tootag kaynak grupları veya VM'ler vardır. Bu doğrudan hello portalından yapabilirsiniz. Veya hello Ekle ResourceSchedule, güncelleştirme ResourceSchedule ve Kaldır-ResourceSchedule runbook'ları kullanabilirsiniz.

### <a name="tag-through-hello-portal"></a>Merhaba Portalı aracılığıyla etiketi
Bu adımları tootag bir sanal makine veya kaynak grubu hello portalında izleyin:

1. Merhaba JSON dizesi düzleştirmek ve boşluk olmayan doğrulayın.  JSON dizenizi aşağıdaki gibi görünmelidir:

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. Select hello **etiketi** simgesi VM veya kaynak grubu tooapply Bu zamanlama.

   ![VM etiketi seçeneği](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. Etiketler, bir anahtar/değer çifti aşağıdaki tanımlanır. Tür **zamanlama** hello içinde **anahtar** alan ve hello JSON dizesi hello yapıştırın **değeri** alan. **Kaydet** düğmesine tıklayın. Yeni etiket şimdi kaynağınız için etiketler hello listesinde gösterilmelidir.

   ![VM zamanlama etiketi](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a>PowerShell etiketinden
Tüm içeri aktarılan runbook'ları nasıl tooexecute hello PowerShell doğrudan runbook'lardan açıklar hello betik hello başında Yardım bilgilerini içerir. Merhaba Ekle ScheduleResource ve güncelleştirme ScheduleResource runbook'lar Powershell'den çağırabilirsiniz. Bunun için bir VM veya kaynak grubundaki hello portal dışında toocreate veya güncelleştirme hello zamanlama etiketi etkinleştirmeniz gerekli parametreleri geçirerek.

toocreate, ekleme ve PowerShell aracılığıyla etiketleri silme, ilk çok gerek[için Azure PowerShell ortamınızı ayarlayın](/powershell/azure/overview). Merhaba kurulumu tamamladıktan sonra aşağıdaki adımları hello ile devam edebilirsiniz.

### <a name="create-a-schedule-tag-with-powershell"></a>PowerShell ile bir zamanlama etiket oluşturma
1. Bir PowerShell oturumu açın. Ardından örnek tooauthenticate farklı çalıştır hesabı ve toospecify bir abonelik aşağıdaki hello kullanın:

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Bir zamanlama karma tablo tanımlayın. Nasıl oluşturulmalıdır örneği şöyledir:

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. Merhaba runbook tarafından gerekli hello parametrelerini tanımlayın. Aşağıdaki örneğine hello biz VM hedeflediğiniz:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    Bir kaynak grubu etiketleme hello kaldırmanız *VMName* hello $params karma parametresinden tablo şu şekilde:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. Merhaba Ekle ResourceSchedule runbook parametreleri toocreate hello zamanlama etiketi aşağıdaki hello ile çalıştırın:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. bir kaynak grubu ya da sanal makineyi etiketi tooupdate yürütme hello **güncelleştirme ResourceSchedule** şu parametreler hello runbook'la:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a>PowerShell ile bir zamanlama Etiketi Kaldır
1. Bir PowerShell oturumu açın ve aşağıdaki farklı çalıştır hesabı ve tooselect tooauthenticate hello çalıştırın ve bir abonelik belirtin:

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. Merhaba runbook tarafından gerekli hello parametrelerini tanımlayın. Aşağıdaki örneğine hello biz VM hedeflediğiniz:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    Bir kaynak grubundan bir etiket kaldırıyorsanız hello kaldırmak *VMName* hello $params karma parametresinden tablo şu şekilde:

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. Merhaba Kaldır ResourceSchedule runbook tooremove hello zamanlama etiketi yürütün:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. tooupdate bir kaynak grubu ya da sanal makineyi etiketi ile şu parametreler hello hello Kaldır ResourceSchedule runbook yürütün:

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> Biz proaktif olarak bu runbook'ları (ve hello sanal makine durumları), sanal makineleriniz yükleniyor tooverify kapatma izlemeniz önerilir ve buna uygun olarak başlatıldı.
>

Azure portal, select hello proje hello tooview hello ayrıntıları hello Test ResourceSchedule runbook'un **işleri** hello runbook parçasına. Hello hello giriş parametreleri iş özeti görüntüler ve hello çıkış akışı, ayrıca hello işle ilgili toogeneral bilgileri ve özel durumlar bunlar ortaya çıktıysa.

Merhaba **iş özeti** hello çıktı, uyarı ve hata akışları gelen iletileri içerir. Select hello **çıkış** tooview döşeme ayrıntılı hello runbook yürütme sonuçları.

![Test ResourceSchedule çıkış](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a>Sonraki adımlar
* PowerShell iş akışı runbook'ları ile başlatılan tooget bkz [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md).
* runbook türleri ve avantajları ve sınırlamaları, hakkında daha fazla toolearn bkz [Azure Automation runbook türleri](automation-runbook-types.md).
* PowerShell betik desteği özellikleri hakkında daha fazla bilgi için bkz: [Azure automation'da yerel PowerShell betik desteği](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).
* runbook günlüğü ve çıktı hakkında daha fazla toolearn bkz [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md).
* bir Azure farklı çalıştır hesabı ve tooauthenticate runbook'larınızın, kullanarak nasıl görürüm hakkında daha fazla toolearn [runbook'ları Azure farklı çalıştır hesabıyla kimlik doğrulaması](automation-sec-configure-azure-runas-account.md).
