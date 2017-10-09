---
title: "aaa\"Düzelt Otomasyon runbook'ları ile Azure VM uyarıları | Microsoft Docs\""
description: "Bu makalede Azure Otomasyon çalışma kitabı ile nasıl toointegrate Azure sanal makine uyarıları gösterir ve sorunları otomatik çözmek"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Azure otomasyonu senaryosu - Azure VM uyarıları Düzelt
Azure Otomasyonu ve Azure sanal makineleri tooconfigure sanal makine (VM) uyarıları toorun Otomasyon runbook'ları sağlayan yeni bir özellik yayımlandı. Bu yeni özellik sağlar tooautomatically yanıt tooVM uyarıları, yeniden başlatma veya durdurma hello VM gibi standart düzeltme gerçekleştirin.

Daha önce VM uyarı kuralı oluşturma sırasında çok girişiminizin[Otomasyonu Web kancası belirtin](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) hello uyarının her sipariş toorun hello runbook tooa runbook'ta. Ancak, bu, toodo hello iş hello runbook oluşturma, hello runbook için hello Web kancası oluşturma ve ardından kopyalama ve uyarı kuralı oluşturma sırasında hello Web kancası yapıştırma gereklidir. Bu yeni sürümle birlikte, çünkü, doğrudan bir runbook bir listeden uyarı kuralı oluşturma sırasında seçebilirsiniz ve hello runbook'u çalıştırmak veya kolayca bir hesap oluşturmasını bir Otomasyon hesabı seçebilir hello işlem daha kolay olur.

Bu makalede, biz ne kadar kolay bir Azure VM uyarı oluşturan tooset olduğunu gösterir ve hello uyarıyı tetikleyen her bir Otomasyon runbook toorun yapılandırın. Örnek senaryolar hello bellek kullanımı hello VM bellek sızıntısı ile tooan uygulama nedeniyle bazı eşiğini aştığında bir VM'yi yeniden başlatırken veya hello CPU kullanıcı zamanı %1 son bir saat boyunca ve kullanımda olmadığında bir VM durdurma içerir. Ayrıca nasıl hello oluşturma otomatik açıklayacağız bir hizmet asıl, Automation hesabı Azure uyarı düzeltme runbook'larda hello kullanımını basitleştirir.

## <a name="create-an-alert-on-a-vm"></a>Bir VM üzerinde bir uyarı oluşturabilir.
Eşiğini sağlandığında adımları tooconfigure bir runbook bir uyarı toolaunch aşağıdaki hello gerçekleştirin.

> [!NOTE]
> Bu sürümle birlikte, yalnızca V2 sanal makineler ve destek için Klasik VM'ler yakında eklenecek destekliyoruz.  
> 
> 

1. Oturum toohello Azure portal ve tıklatın **sanal makineleri**.  
2. Sanal makinelerinizi birini seçin.  Merhaba sanal makine Pano dikey görünür hello ve **ayarları** dikey tooits sağ.  
3. Merhaba gelen **ayarları** hello izleme bölümü seçin altında dikey **uyarı kuralları**.
4. Merhaba üzerinde **uyarı kuralları** dikey penceresinde tıklatın **uyarı Ekle**.

Merhaba açılır **uyarı kuralı eklemek** burada hello uyarı hello koşulları yapılandırmak ve aşağıdakilerden birini veya bu seçeneklerin tümü arasında seçin dikey: e-posta toosomeone göndermek, bir Web kancası tooforward hello uyarı tooanother sistemi kullanmak ve/veya bir Otomasyon runbook'u yanıt girişimi tooremediate hello sorunu çalıştırın.

## <a name="configure-a-runbook"></a>Bir runbook yapılandırma
tooconfigure hello VM uyarı eşiği karşılandığında, bir runbook toorun seçin **Otomasyon Runbook'u**. Merhaba, **runbook yapılandırma** dikey penceresinde hello runbook toorun ve hello Otomasyon hesabı toorun hello runbook'ta seçebilirsiniz.

![Otomasyon runbook yapılandırma ve yeni bir Otomasyon hesabı oluşturma](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> Bu sürüm için hello hizmet sağlayan – üç runbook'lardan VM yeniden başlatma, durdurma VM veya kaldırma VM seçebilirsiniz (silme).  diğer runbook'lar özelliği tooselect hello veya kendi runbook'ları biri gelecekteki bir sürümde kullanılabilir olacaktır.
> 
> 

![Runbook'ları toochoose gelen](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Merhaba üç kullanılabilir runbook'ları birini seçtikten sonra hello **Otomasyon hesabı** aşağı açılan listesi görüntülenir ve bir Otomasyon seçebilirsiniz hesap hello runbook olarak çalışır. Runbook'lar gerek toorun hello bağlamındaki bir [Otomasyon hesabı](automation-security-overview.md) Azure aboneliğinizde olmasıdır. Önceden oluşturulmuş veya sizin için oluşturulan yeni bir Otomasyon hesabı olabilir bir Otomasyon hesabı seçebilirsiniz.

sağlanan hello runbook'ları tooAzure hizmet sorumlusunu kullanarak kimlik doğrulaması. Toorun hello runbook, var olan Otomasyon hesaplarından birini seçerseniz, otomatik olarak hello hizmet asıl sizin için oluşturacağız. Yeni bir Otomasyon hesabı toocreate seçerseniz, ardından otomatik olarak hello hesabı ve hello hizmet sorumlusu oluşturacağız. Her iki durumda da, iki varlıklar da hello Otomasyon hesabı – adlı bir sertifika varlığı oluşturulacak **AzureRunAsCertificate** ve adlı bir bağlantı varlığı **AzureRunAsConnection**. Merhaba runbook'ları kullanacak **AzureRunAsConnection** sipariş tooperform hello Yönetimi eylem hello VM karşı Azure ile tooauthenticate.

> [!NOTE]
> Merhaba hizmet sorumlusu hello abonelik kapsamında oluşturulan ve hello katkıda bulunan rolü atanır. Bu rol, sırayla hello hesap toohave izin toorun Otomasyon runbook'ları toomanage Azure VM'ler için gereklidir.  Merhaba oluşturulmasını Automaton hesabı ve/veya hizmet sorumlusu tek seferlik bir olaydır. Oluşturulduktan sonra diğer Azure VM uyarılar için bu hesabı toorun runbook'ları kullanabilirsiniz.
> 
> 

Tıkladığınızda **Tamam** hello uyarı yapılandırılır ve hello seçeneği toocreate yeni bir Otomasyon hesabı seçtiyseniz, bu hello hizmet sorumlusu birlikte oluşturulur.  Bu işlem birkaç saniye sürebilir toocomplete.  

![Yapılandırılmakta Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Merhaba Yapılandırma tamamlandıktan sonra hello adını hello görünür hello runbook görürsünüz **uyarı kuralı eklemek** dikey.

![Yapılandırılmış Runbook](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Tıklatın **Tamam** hello içinde **uyarı kuralı eklemek** dikey penceresinde ve hello uyarı kuralı oluşturulur ve hello sanal makine çalışır durumda ise etkinleştirin.

### <a name="enable-or-disable-a-runbook"></a>Etkinleştirmek veya devre dışı bir runbook
Bir uyarı için yapılandırılmış bir runbook'unuz varsa, onu hello runbook yapılandırma kaldırmadan devre dışı bırakabilirsiniz. Bu çalışan tookeep hello uyarı verir ve belki de hello uyarı kuralları bazılarını test ve daha sonra hello runbook yeniden etkinleştirin.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Azure uyarı ile çalışan bir runbook'u oluşturma
Bir Azure uyarı kuralının bir parçası bir runbook seçtiğinizde hello runbook toohave mantığında tooit geçirilen toomanage hello uyarı verileri gerekir.  Bir runbook bir uyarı kuralı yapılandırıldığında, bir Web kancası hello runbook için oluşturulur; her zaman hello uyarı Tetikleyicileri runbook kullanılan toostart hello sonra o Web kancası olur.  Merhaba gerçek çağrısını toostart hello runbook bir HTTP POST isteği toohello Web kancası URL'dir. Merhaba POST isteği Hello gövdesini yararlı özellikleri ilgili toohello uyarı içeren bir JSON biçiminin nesnesi içerir.  Aşağıda görüldüğü gibi hello uyarı verileri Subscriptionıd, resourceGroupName, resourceName ve resourceType gibi ayrıntıları içerir.

### <a name="example-of-alert-data"></a>Uyarı veri örneği
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

Merhaba Otomasyonu Web kancası hizmeti hello HTTP POST aldığında hello uyarı verileri ayıklar ve toohello runbook hello WebhookData runbook giriş parametresi geçirir.  Nasıl toouse WebhookData parametresi hello hello uyarı verileri ayıklamak ve toomanage hello hello uyarıyı tetikleyen Azure kaynak kullanmak gösteren bir örnek runbook aşağıdadır.

### <a name="example-runbook"></a>Örnek runbook
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a>Özet
Azure VM temelinde bir uyarı yapılandırırken bir Otomasyon yapılandırma hello özelliği tooeasily şimdi sahip runbook tooautomatically hello uyarıyı tetikleyen zaman düzeltme eylemi gerçekleştirir. Bu sürüm için runbook'ları toorestart seçebilirsiniz, durdurmak veya uyarı senaryonuza bağlı olarak bir VM silme. Bu uyarıyı tetikleyen olduğunda otomatik olarak gerçekleştirilecek hello eylemleri (bildirim, sorun giderme, düzeltme) kontrol burada senaryoları etkinleştirme yalnızca hello başlangıçtır.

## <a name="next-steps"></a>Sonraki Adımlar
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)
* runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla toolearn bakın [Azure Automation runbook türleri](automation-runbook-types.md)

