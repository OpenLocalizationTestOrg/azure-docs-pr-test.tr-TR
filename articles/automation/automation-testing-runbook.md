---
title: Azure Automation runbook aaaTesting | Microsoft Docs
description: "Azure Otomasyonu runbook'u yayımlamadan önce beklendiği gibi çalıştığını tooensure test edebilirsiniz.  Bu makalede nasıl tootest bir runbook ve çıktısını görüntüleyin."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Azure Otomasyonu runbook'u test etme
Bir runbook'u test ettiğinizde hello [taslak sürüm](automation-creating-importing-runbook.md#publishing-a-runbook) yürütülür ve gerçekleştirdiği tüm işlemler tamamlanır. İş geçmişi yok oluşturuldu, ancak hello [çıkış](automation-runbook-output-and-messages.md#output-stream) ve [uyarı ve hata](automation-runbook-output-and-messages.md#message-streams) akışları görüntülenir hello Test bölmesi çıktısı. İletileri toohello [ayrıntılı akış](automation-runbook-output-and-messages.md#message-streams) hello çıkış bölmesi yalnızca hello görüntülenir [$VerbosePreference değişkeni](automation-runbook-output-and-messages.md#preference-variables) tooContinue ayarlanır.

Hello taslak sürüm çalıştırılır olsa bile, hello runbook hala hello akışını normal olarak yürütür ve işlemleri ortamdaki kaynakları hello ortamında gerçekleştirir. Bu nedenle, yalnızca üretim dışı kaynaklar runbook'ları test etmeniz gerekir.

yordam tootest hello [runbook türü](automation-runbook-types.md) aynı hello ve hello metin düzenleyicisini hello grafik Düzenleyicisi'nde hello Azure portal arasındaki sınamada fark yoktur.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest bir runbook'ta hello Azure portalı
Tüm iş [runbook türü](automation-runbook-types.md) hello Azure Portalı'nda.

1. Her iki hello hello runbook'ta açık hello taslak sürümünü [metin düzenleyicisini](automation-edit-textual-runbook.md) veya [grafik Düzenleyicisi](automation-graphical-authoring-intro.md).
2. Merhaba tıklatın **Test** düğmesini tooopen hello Test dikey penceresini.
3. Merhaba runbook'un parametreleri varsa, burada hello test için kullanılan değerleri toobe sağlayabilir hello sol bölmede listelenir.
4. Toorun hello test istiyorsanız bir [karma Runbook çalışanı](automation-hybrid-runbook-worker.md), ardından değiştirme **çalıştırma ayarları** çok**karma çalışanı** ve select hello hello hedef grubun adı.  Aksi takdirde hello varsayılan tutmak **Azure** toorun hello test hello bulutta.
5. Merhaba tıklatın **Başlat** düğmesini toostart hello test.
6. Merhaba runbook ise [PowerShell iş akışı](automation-runbook-types.md#powershell-workflow-runbooks) veya [grafik](automation-runbook-types.md#graphical-runbooks), durdurmak veya hello çıkış bölmesi altında hello düğmeleri ile bu test devam ederken askıya alma. Merhaba runbook'u askıya aldığınızda, askıya alınmadan önce hello geçerli etkinliği tamamlar. Merhaba runbook askıya alındığında, durdurabilir veya yeniden başlatın.
7. Merhaba runbook hello çıkış bölmesinde Hello çıktısını inceleyin.

## <a name="next-steps"></a>Sonraki Adımlar
* toocreate veya içeri aktarma bir runbook nasıl görürüm toolearn [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md)
* Grafik yazma hakkında daha fazla toolearn bakın [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md)
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)
* runboks tooreturn durum iletilerini ve hataların önerilen yöntemleri de dahil olmak üzere, yapılandırma hakkında daha fazla toolearn bkz [Runbook çıkışı ve iletileri Azure Automation](automation-runbook-output-and-messages.md)

