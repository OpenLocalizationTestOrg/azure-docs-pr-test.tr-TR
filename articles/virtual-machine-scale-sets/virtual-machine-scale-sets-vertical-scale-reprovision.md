---
title: "aaaVertically ölçek Azure sanal makine ölçek kümeleri | Microsoft Docs"
description: "Nasıl toovertically ölçeklendirme bir sanal makine yanıt toomonitoring uyarılar Azure Automation"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Sanal makine ölçek kümeleri ile dikey otomatik ölçeklendirme
Nasıl toovertically ölçeklendirme Azure bu makalede [sanal makine ölçek kümeleri](https://azure.microsoft.com/services/virtual-machine-scale-sets/) ile veya sağlama işleminin olmadan. Dikey Ölçek kümelerinde olmayan vm'lere ölçekleme için çok başvuran[Azure Automation ile Azure sanal makine dikey olarak ölçeklendirmek](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Dikey olarak da bilinen ölçeklendirme, *ölçeği* ve *ölçeklendirmeyi azaltın*, artan veya azalan yanıt tooa iş yükü sanal makine (VM) boyutları anlamına gelir. Bu karşılaştırma [yatay ölçekleme](virtual-machine-scale-sets-autoscale-overview.md), tooas ya da *ölçeğini* ve *içinde ölçeklendirmek*, VM'lerin sayısını hello hello iş yüküne bağlı olarak burada değiştirilemez.

Sağlama işleminin, mevcut bir VM'yi kaldırarak ve yeni bir tane ile değiştirerek anlamına gelir. Artırın veya VM ölçek kümesindeki sanal makineleri hello boyutunu azaltın, bazı durumlarda, VM'ler varolan tooresize istediğiniz ve diğer durumlarda toodeploy gerekirken, verilerinizi korumak hello yeni boyutunu yeni VM'ler. Bu belge her iki durumda da kapsar.

Dikey ölçekleme durumlarda yararlı olabilir:

* Sanal makineler üzerinde oluşturulmuş bir (örneğin sonları) altında kullanılan hizmetidir. Merhaba VM boyutunun azaltılması aylık maliyetlerini azaltabilir.
* VM boyutu toocope büyük talep ek sanal makineleri oluşturmadan artırma.

Dikey ayarlayabilirsiniz tetiklenen toobe ölçeklendirme temel ölçüm tabanlı uyarılardan VM ölçek kümesi. Merhaba uyarı etkinleştirildiğinde, bir Web Kancası Yukarı veya aşağı, Ölçek ölçeklenebilen bir runbook ayarlamak bu Tetikleyicileri tetikler. Dikey ölçeklendirme, aşağıdaki adımları izleyerek yapılandırılabilir:

1. Çalıştır özelliğine sahip bir Azure Otomasyonu hesabı oluşturun.
2. Azure Otomasyonu dikey ölçek runbook'ları VM ölçek kümesi için aboneliğinizi alın.
3. Bir Web kancası tooyour runbook ekleyin.
4. Bir uyarı tooyour bir Web kancası bildirim kullanarak VM ölçek kümesi ekleyin.

> [!NOTE]
> Dikey otomatik ölçeklendirmeyi yalnızca belirli aralıklarında VM boyutları gerçekleşebilir. Bir tooanother gelen tooscale karar vermeden önce her boyutta Hello belirtimleri karşılaştırma (daha yüksek sayı her zaman belirtmez büyük VM boyutu). Tooscale boyutları çiftlerini aşağıdaki hello arasında seçim yapabilirsiniz:
> 
> | VM boyutları çifti ölçeklendirme |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Çalıştır özelliğine sahip Azure Automation hesabı oluşturma
toodo ihtiyacınız hello ilk hello kullanılan runbook'ları tooscale hello VM ölçek kümesi örneklerinin barındıracak Azure Automation hesabı oluşturma şeydir. Yakın zamanda [Azure Otomasyonu](https://azure.microsoft.com/services/automation/) otomatik olarak hello çalışan runbook'ları bir kullanıcı adına çok kolay için hello hizmet sorumlusu ayarlama kılan hello "Farklı Çalıştır hesabı" özellik sunulmuştur. Daha fazla bilgiyi bu konuda aşağıdaki hello makale:

* [Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Aboneliğinizi Azure Otomasyon dikey ölçek runbook'ları alma
Merhaba runbook'ları VM ölçek kümesi zaten hello Azure Otomasyonu Runbook Galerisi yayımlanan toovertically ölçek gerekli. aboneliğinizi bunlara hello izleyin tooimport bu makaledeki adımları:

* [Azure Otomasyonu Runbook ve modül galerileri](../automation/automation-runbook-gallery.md)

Merhaba Runbook'lar menüsünden Hello Gözat galeri seçenek belirleyin:

![İçe aktarılan Runbook'lar toobe][runbooks]

toobe alınan ihtiyacınız hello runbook'lar gösterilir. Merhaba runbook olup, Ölçek ile veya olmadan sağlama işleminin dikey istediğinize bağlı seçin:

![Runbook Galerisi][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Web kancası tooyour runbook Ekle
Merhaba runbook'ları içe sonra bir VM ölçek kümesi bir uyarıdan tarafından tetiklenebilir şekilde tooadd bir Web kancası toohello runbook gerekir. Bu makalede, Runbook için bir Web kancası oluşturma hello ayrıntıları açıklanmaktadır:

* [Azure Otomasyonu Web kancası](../automation/automation-webhooks.md)

> [!NOTE]
> Bu hello sonraki bölümde ihtiyaç duyacağınız hello Web kancası iletişim kutusunu kapatmadan önce hello Web kancası URI kopyaladığınızdan emin olun.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Bir uyarı tooyour VM ölçek kümesi Ekle
Bir PowerShell betiğini hangi gösterir nasıl aşağıdadır tooadd bir uyarı tooa VM ölçek kümesi. Makale tooget hello hello ölçüm toofire hello uyarı adını aşağıdaki toohello bakın: [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> Bu dikey ölçekleme tetikleme sırasını tooavoid hello uyarıda için makul zaman penceresi tooconfigure önerilen ve herhangi bir hizmet kesintisi, çok sık ilişkilendirilmiş. Pencerenin en az 20-30 dakika veya daha fazla göz önünde bulundurun. Herhangi bir kesintiye tooavoid gerekiyorsa ölçeklendirme yatay göz önünde bulundurun.
> 
> 

Nasıl toocreate uyarıları makaleler toohello başvurmak hakkında daha fazla bilgi için:

* [Azure İzleyici PowerShell hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Özet
Bu makalede basit dikey ölçekleme örnekler gösterilmiştir. Bu yapı taşları ile - Automation hesabı, runbook'ları, Web kancalarını, uyarıları - zengin olayları çeşitli eylemler özelleştirilmiş bir dizi bağlanabilir.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
