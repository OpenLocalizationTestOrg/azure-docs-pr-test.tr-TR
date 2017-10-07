---
title: "aaaVertically ölçek Azure Automation ile Azure sanal makine | Microsoft Docs"
description: "Nasıl toovertically ölçeklendirme Linux sanal makine yanıt toomonitoring uyarılar Azure Automation"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a>Dikey olarak Azure Automation ile Azure Linux sanal makine ölçekleme
Dikey ölçekleme artan veya azalan bir makine yanıt toohello iş yükü hello kaynakları hello işlemidir. Azure'da bu hello hello sanal makine boyutunu değiştirerek gerçekleştirilebilir. Bu senaryolar aşağıdaki hello yardımcı olabilir

* Sanal makine Hello sık kullanılmayan, tooa daha küçük boyutu tooreduce aylık maliyetleriniz yeniden boyutlandırabilirsiniz
* Sanal makine Hello yoğun yük görmesini yoksa, yapabilirsiniz yeniden boyutlandırılan tooa büyük boyutu tooincrease kapasitesi olabilir

Merhaba anahat budur olarak hello adımları tooaccomplish için aşağıda

1. Azure Otomasyonu tooaccess sanal makinelerinizi Kurulumu
2. Aboneliğinizi Hello Azure Otomasyon dikey ölçek runbook'ları alma
3. Web kancası tooyour runbook Ekle
4. Bir uyarı tooyour sanal makine ekleyin

> [!NOTE]
> İlk sanal makine, bunu ölçeklendirilmiş için hello boyutları hello Hello boyutu nedeniyle sınırlanabilir hello toohello kullanılabilirliği, içinde geçerli sanal makine hello kümedeki diğer boyutlara dağıtılır. Bu durumda ilgilenebilmek ve yalnızca VM boyutu çiftleri aşağıda hello içinde ölçeklendirmek bu makalede kullanılan Otomasyon runbook'ları Hello yayımladı. Bu bir Standard_D1v2 sanal makine değil aniden tooStandard_G5 ölçeklendirilemez ya da tooBasic_A0 ölçeklendirilmiş olduğunu anlamına gelir.
> 
> | VM boyutları çifti ölçeklendirme |  |
> | --- | --- |
> | Basic_A0 |Basic_A4 |
> | Standard_A0 |Standard_A4 |
> | Standard_A5 |Standard_A7 |
> | Standard_A8 |Standard_A9 |
> | Standard_A10 |Standard_A11 |
> | Standard_D1 |Standard_D4 |
> | Standard_D11 |Standard_D14 |
> | Standard_DS1 |Standard_DS4 |
> | Standard_DS11 |Standard_DS14 |
> | Standard_D1v2 |Standard_D5v2 |
> | Standard_D11v2 |Standard_D14v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a>Azure Otomasyonu tooaccess sanal makinelerinizi Kurulumu
toodo ihtiyacınız hello ilk hello kullanılan runbook'ları tooscale hello VM ölçek kümesi örneklerinin barındıracak Azure Automation hesabı oluşturma şeydir. Yakın zamanda hello Otomasyon hizmeti otomatik olarak hello çalışan runbook'ları hello kullanıcı adına çok kolay için hello hizmet sorumlusu ayarlama kılan hello "Farklı Çalıştır hesabı" özellik sunulmuştur. Daha fazla bilgiyi bu konuda aşağıdaki hello makale:

* [Azure Farklı Çalıştır hesabıyla Runbook Kimlik Doğrulaması](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Aboneliğinizi Hello Azure Otomasyon dikey ölçek runbook'ları alma
Sanal makineniz zaten hello Azure Otomasyonu Runbook Galerisi yayımlanan dikey ölçekleme için gerekli olan hello runbook'ları. Tooimport gerekir, aboneliğe bunları. Makalede okuyarak tooimport runbook'ları nasıl hello öğrenebilirsiniz.

* [Azure Otomasyonu Runbook ve modül galerileri](../../automation/automation-runbook-gallery.md)

Aşağıdaki hello görüntü toobe alınan ihtiyacınız hello runbook'lar gösterilir

![Runbook'ları alma](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a>Web kancası tooyour runbook Ekle
Merhaba runbook'ları içe sonra bir sanal makineden bir uyarı tarafından tetiklenebilir şekilde tooadd bir Web kancası toohello runbook gerekir. Runbook için bir Web kancası oluşturma hello ayrıntıları buraya okuyabilir

* [Azure Otomasyonu Web kancası](../../automation/automation-webhooks.md)

Bu hello sonraki bölümde ihtiyaç duyacağınız hello Web kancası iletişim kutusunu kapatmadan önce hello Web kancası kopyaladığınızdan emin olun.

## <a name="add-an-alert-tooyour-virtual-machine"></a>Bir uyarı tooyour sanal makine ekleyin
1. Sanal makine ayarlarını seçin
2. "Uyarı kuralları" seçeneğini belirleyin
3. "Uyarı Ekle" seçin
4. Ölçüm toofire hello uyarıyı seçin
5. Bir koşul Seç hangi olduğunda yerine hello uyarı toofire neden
6. Adım 5'te hello koşul için bir eşik seçin. yerine toobe
7. İzleme hizmeti hangi hello denetleyecek bir dönem için hello koşul ve eşik adımları 5 ve 6'seçin
8. Merhaba önceki bölümünde kopyaladığınız hello Web kancası yapıştırın.

![Uyarı tooVirtual makine 1 ekleme](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![Uyarı tooVirtual makine 2 ekleme](./media/vertical-scaling-automation/add-alert-webhook-2.png)

