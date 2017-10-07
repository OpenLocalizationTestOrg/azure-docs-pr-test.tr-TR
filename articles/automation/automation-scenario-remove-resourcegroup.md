---
title: "Kaynak grupları aaaAutomate kaldırılmasını | Microsoft Docs"
description: "PowerShell iş akışı runbook'ları tooremove dahil olmak üzere bir Azure otomasyonu senaryosu sürümü aboneliğinizde tüm kaynak grupları."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Azure Otomasyonu senaryosu - kaynak gruplarının kaldırılmasını otomatik hale getirme
Birçok müşteri birden fazla kaynak grubu oluşturur. Bazıları üretim uygulamalarını yönetmek için, bazıları ise geliştirme, test ve hazırlık ortamları olarak kullanılabilir. Bu kaynaklar Hello dağıtımını otomatik hale getirme tek şey, ancak mümkün toodecommission bir düğmeyi tıklatarak, hello sahip bir kaynak grubu olan başka bir. Bu ortak yönetim görevini Azure Otomasyonu'nu kullanarak basit hale getirebilirsiniz. Bu üye teklifi MSDN veya hello Microsoft iş ortağı ağı Bulut Temel programı gibi aracılığıyla bir harcama sınırına sahip bir Azure aboneliği ile çalışıyorsanız yararlıdır.

Bu senaryo, bir PowerShell runbook temel alır ve tasarlanmış tooremove aboneliğinizden belirttiğiniz bir veya daha fazla kaynak grupları değil. Merhaba varsayılan hello runbook devam etmeden önce tootest ayarıdır. Bu, hazır toocomplete olmadan önce yanlışlıkla hello kaynak grubu bu yordamı silmeyin olmasını sağlar.   

## <a name="getting-hello-scenario"></a>Merhaba senaryo alma
Bu senaryo hello indirebilirsiniz bir PowerShell runbook oluşur [PowerShell Galerisi](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript). Ayrıca, doğrudan hello da içeri aktarabilirsiniz [Runbook Galerisi](automation-runbook-gallery.md) hello Azure Portalı'nda.<br><br>

| Runbook | Açıklama |
| --- | --- |
| Remove-ResourceGroup |Bir veya daha fazla Azure kaynak gruplarını ve ilişkili kaynakları hello abonelikten kaldırır. |

<br>
Giriş parametreleri aşağıdaki hello bu runbook için tanımlanmıştır:

| Parametre | Açıklama |
| --- | --- |
| NameFilter (Gerekli) |Düşündüğünüz bir adı filtre toolimit hello kaynak gruplarını silmeye ilişkin belirtir. Virgülle ayrılmış bir liste kullanarak birden çok değer geçirebilirsiniz.<br>Merhaba filtre büyük küçük harfe duyarlı değildir ve hello dizeyi içeren herhangi bir kaynak grubu ile eşleşir. |
| PreviewMode (İsteğe bağlı) |Kaynak grupları silinecek, ancak hiçbir eylemde hello runbook toosee yürütür.<br>Merhaba varsayılandır **true** toohelp birini yanlışlıkla silinmesini önlemek veya daha fazla kaynak grupları toohello runbook geçirildi. |

## <a name="install-and-configure-this-scenario"></a>Bu senaryoyu yükleme ve yapılandırma
### <a name="prerequisites"></a>Ön koşullar
Bu runbook hello kullanarak kimlik doğrulaması [Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md).    

### <a name="install-and-publish-hello-runbooks"></a>Yükleme ve yayımlama hello runbook'ları
Merhaba runbook indirdikten sonra onu hello yordamı kullanarak içeri aktarabilirsiniz [runbook yordamlar alınıyor](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation). Otomasyon hesabınızda başarıyla alındıktan sonra hello runbook yayımlayın.

## <a name="using-hello-runbook"></a>Merhaba runbook kullanma
Merhaba aşağıdaki adımları, bu runbook ve nasıl çalıştığı ile aşina Yardım hello yürütülmesini rehberlik yapar. Yalnızca hello runbook Bu örnekte, aslında hello kaynak grubunun silinmesi test.  

1. Hello Azure portal, Automation hesabınızı açın ve'ı tıklatın **Runbook'lar**.
2. Select hello **Kaldır ResourceGroup** runbook tıklatıp **Başlat**.
3. Merhaba runbook'u başlattığınızda hello **Runbook'u Başlat** dikey penceresi açılır ve hello parametrelerini yapılandırabilirsiniz. Kaynak grupları Hello adlarını test kullanabilirsiniz ve hiçbir zarar yanlışlıkla sildiyseniz neden olur, aboneliğinizde girin.<br> ![Remove-ResouceGroup parametreleri](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > Emin olun **Previewmode** çok ayarlanır**true** hello silme tooavoid seçilen kaynak grupları.  **Not** bu runbook bu runbook'un çalıştığı hello Otomasyon hesabını içeren hello kaynak grubu kaldırmaz.  
   >
   >
4. Tüm hello parametre değerleri yapılandırdıktan sonra tıklatın **Tamam**, ve hello runbook yürütme için sıraya.  

Merhaba tooview hello ayrıntılarını **Kaldır ResourceGroup** hello Azure portal, select runbook işi **işleri** hello runbook'taki. Ayrıca Hello hello giriş parametreleri iş özeti görüntüler ve hello çıktı hello işle ilgili toogeneral bilgileri ve oluşan tüm özel durumları akış.<br> ![Remove-ResourceGroup runbook iş durumu](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png).

Merhaba **iş özeti** hello çıktı, uyarı ve hata akışları gelen iletileri içerir. Seçin **çıkış** tooview ayrıntılı hello runbook yürütme sonuçları.<br> ![Remove-ResourceGroup runbook çıkış sonuçları](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>Sonraki adımlar
* kendi runbook oluşturmaya başlamanızı tooget bkz [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md).
* PowerShell iş akışı runbook'ları ile çalışmaya tooget bkz [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md).
