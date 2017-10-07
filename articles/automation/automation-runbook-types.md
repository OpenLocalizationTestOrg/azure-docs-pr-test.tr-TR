---
title: "aaaAzure Automation Runbook türleri | Microsoft Docs"
description: "Azure Automation ve hangi tür toouse belirlerken dikkate almanız konuları kullanabilirsiniz runbook'ları Hello farklı türleri açıklanmaktadır. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Azure Automation runbook türleri
Azure Otomasyonu, aşağıdaki tablonun hello kısaca açıklanmıştır runbook'ları dört türlerini destekler.  Merhaba aşağıdaki bölümlerde verilmektedir etkin olduğunda dikkat edilecek noktalar dahil her tür hakkında daha fazla bilgi toouse her.

| Tür | Açıklama |
|:--- |:--- |
| [Grafik](#graphical-runbooks) |Windows PowerShell ve Azure portalında oluşturulan ve tamamen içinde düzenlenen grafik Düzenleyicisi göre. |
| [Grafik PowerShell iş akışı](#graphical-runbooks) |Windows PowerShell iş akışı ve Azure portalında oluşturulan ve tamamen içinde düzenlenen hello grafik Düzenleyicisi göre. |
| [PowerShell](#powershell-runbooks) |Windows PowerShell komut dosyasına dayalı metin runbook. |
| [PowerShell İş Akışı](#powershell-workflow-runbooks) |Windows PowerShell iş akışı tabanlı metin runbook. |

## <a name="graphical-runbooks"></a>Grafik runbook'lar
[Grafik](automation-runbook-types.md#graphical-runbooks) ve grafik PowerShell iş akışı runbook'ları oluşturulur ve hello grafik Düzenleyicisi'nde hello Azure portal ile düzenlenemez.  Tooa dosyasını dışarı aktarmak ve ardından başka bir Otomasyon hesaba içeri aktarmak, ancak oluşturamaz veya bunları başka bir araçla düzenleyin.  PowerShell kodu grafik runbook'ları oluşturmak, ancak doğrudan görüntüleyemez veya hello kodu değiştirin. Grafik runbook'lar Merhaba, dönüştürülmüş tooone olamaz [metin biçimleri](automation-runbook-types.md), veya bir metin runbook dönüştürülmüş toographical biçimi olabilir. Grafik runbook'lar dönüştürülmüş tooGraphical PowerShell iş akışı runbook'ları içeri aktarma ve tam tersini sırasında olabilir.

### <a name="advantages"></a>Avantajları
* INSERT bağlantısını yapılandırmak görsel geliştirme modeli  
* Veri hello süreci nasıl akacağını odaklanın  
* Yönetim işlemlerini görsel olarak temsil eder  
* Alt runbook'ları toocreate yüksek düzey iş akışları olarak diğer runbook'lar içerir  
* Modüler programlama teşvik eder  


### <a name="limitations"></a>Sınırlamalar
* Azure portal dışında runbook'u düzenleyemez.
* PowerShell kodu tooperform karmaşık mantığı içeren bir kod etkinlik gerektirebilir.
* Görüntüleyemez veya doğrudan hello grafik iş akışı tarafından oluşturulan hello PowerShell kodunu düzenleyemezsiniz. Hiçbir kod etkinliklerin oluşturduğunuz hello kodu görüntüleyebilirsiniz unutmayın.

## <a name="powershell-runbooks"></a>PowerShell runbook'ları
PowerShell runbook'ları Windows PowerShell üzerinde temel alır.  Doğrudan başlangıç kodunu hello Azure portal hello metin düzenleyicisi kullanarak hello runbook'un düzenleyin.  Herhangi bir çevrimdışı metin düzenleyicisi de kullanabilirsiniz ve [hello runbook'u içeri](http://msdn.microsoft.com/library/azure/dn643637.aspx) Azure Otomasyonu içine.

### <a name="advantages"></a>Avantajları
* PowerShell iş akışı hello ek karmaşıklığını olmadan PowerShell kodu ile tüm karmaşık mantığı uygular. 
* Çalıştırmadan önce derlenmiş toobe gerekli olmayan beri Runbook PowerShell iş akışı runbook'ları daha hızlı başlatır.

### <a name="limitations"></a>Sınırlamalar
* PowerShell komut dosyalarıyla bilgi sahibi olmanız gerekir.
* Kullanamazsınız [paralel işleme](automation-powershell-workflow.md#parallel-processing) tooperform paralel birden çok eylem.
* Kullanamazsınız [kontrol noktaları](automation-powershell-workflow.md#checkpoints) tooresume runbook hata durumunda.
* PowerShell iş akışı runbook'ları ve grafik runbook'lar yalnızca yeni bir işi oluşturan hello başlangıç AzureAutomationRunbook cmdlet'ini kullanarak alt runbook'lar olarak eklenebilir.

### <a name="known-issues"></a>Bilinen sorunlar
PowerShell runbook'ları bilinen geçerli sorunlar aşağıda verilmiştir.

* PowerShell runbook'ları olamaz alamıyor bir şifrelenmemiş [değişken varlığı](automation-variables.md) null değerine sahip.
* PowerShell runbook'ları alamıyor bir [değişken varlığı](automation-variables.md) ile  *~*  hello adı.
* Get-Process döngü olarak bir PowerShell runbook yaklaşık 80 yinelemeden sonra kilitlenebilir. 
* Bir PowerShell runbook toowrite çok büyük miktarda veri toohello çıkış akışı aynı anda çalışırsa başarısız olabilir.   Bu sorunu çözmek yalnızca büyük nesneler ile çalışırken, gereksinim hello bilgileri kayıt çıkarma genellikle çalışabilir.  Örneğin, aşağıdakine benzer çıktısı yerine *Get-Process*, yalnızca gerekli hello alanlarla çıkarabilirsiniz *Get-Process | İşlem adı, CPU seçin*.

## <a name="powershell-workflow-runbooks"></a>PowerShell iş akışı runbook'ları
PowerShell iş akışı runbook'ları olan temel metin runbook'lar [Windows PowerShell iş akışı](automation-powershell-workflow.md).  Doğrudan başlangıç kodunu hello Azure portal hello metin düzenleyicisi kullanarak hello runbook'un düzenleyin.  Herhangi bir çevrimdışı metin düzenleyicisi de kullanabilirsiniz ve [hello runbook'u içeri](http://msdn.microsoft.com/library/azure/dn643637.aspx) Azure Otomasyonu içine.

### <a name="advantages"></a>Avantajları
* PowerShell iş akışı kodu ile tüm karmaşık mantığı uygular.
* Kullanım [kontrol noktaları](automation-powershell-workflow.md#checkpoints) tooresume runbook hata durumunda.
* Kullanım [paralel işleme](automation-powershell-workflow.md#parallel-processing) tooperform paralel birden çok eylem.
* Diğer grafik runbook'lar ve PowerShell iş akışı runbook alt runbook'ları toocreate yüksek düzey iş akışları olarak ekleyebilirsiniz.

### <a name="limitations"></a>Sınırlamalar
* Yazar PowerShell iş akışı ile bilgi sahibi olmanız gerekir.
* Runbook gerekir Dağıt hello ek karmaşıklığını PowerShell iş akışı ile gibi [nesneleri seri durumdan](automation-powershell-workflow.md#code-changes).
* Çalıştırmadan önce derlenmiş toobe gerektiğinden Runbook PowerShell runbook'ları daha uzun toostart alır.
* PowerShell runbook'ları yalnızca yeni bir işi oluşturan hello başlangıç AzureAutomationRunbook cmdlet'ini kullanarak alt runbook'lar olarak eklenebilir.

## <a name="considerations"></a>Dikkat edilmesi gerekenler
Ek hususlar belirli bir runbook için hangi tür toouse belirlerken aşağıdaki hesap hello içine almanız gerekir.

* Runbook, grafik tootextual türü ya da tam tersini dönüştürülemiyor.
* Farklı türdeki runbook'lar bir alt runbook'u kullanarak sınırlamalar vardır.  Bkz: [alt runbook'ları Azure Automation](automation-child-runbooks.md) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
* Grafik runbook yazma, hakkında daha fazla toolearn bakın [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md)
* toounderstand Merhaba, runbook'lar için iş akışlarını PowerShell ve PowerShell farklar için bkz: [öğrenme Windows PowerShell iş akışı](automation-powershell-workflow.md)
* Toocreate veya içeri aktarma bir Runbook nasıl görürüm hakkında daha fazla bilgi için [oluşturma veya bir Runbook'u içeri aktarma](automation-creating-importing-runbook.md)

