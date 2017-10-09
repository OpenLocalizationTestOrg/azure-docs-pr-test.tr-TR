---
title: "Azure Otomasyonu aaaRunbook ve modülü galerileri | Microsoft Docs"
description: "Runbook'lardan ve modüllerden Microsoft ve hello topluluktan, tooinstall için kullanılabilir ve Azure Otomasyonu ortamınızda kullanın.  Bu makalede, runbook'ları toohello galeri nasıl bu kaynakları ve toocontribute erişebileceğiniz açıklanır."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Azure Otomasyonu Runbook ve modül galerileri
Azure Automation'da kendi runbook'lardan ve modüllerden oluşturmak yerine, çeşitli Microsoft ve hello topluluk tarafından zaten oluşturulmuş senaryoları erişebilir.  Bu senaryolar değişiklik yapmadan ya da kullanabilir veya bir başlangıç noktası olarak kullanın ve bunları belirli gereksinimleriniz için düzenleyin.

Runbook'ları hello elde edebilirsiniz [Runbook Galerisi](#runbooks-in-runbook-gallery) ve hello modüllerden [PowerShell Galerisi](#modules-in-powerShell-gallery).  Ayrıca geliştirme senaryoları paylaşarak toohello topluluğa katkıda bulunabilir.

## <a name="runbooks-in-runbook-gallery"></a>Runbook Galerisi runbook'ları
Merhaba [Runbook Galerisi](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) Azure Automation'a aktarabilirsiniz Microsoft ve hello topluluktan runbook'ları çeşitli sağlar. Hello barındırılan hello Galeriden bir runbook indirebilirsiniz [TechNet Komut Merkezi](https://gallery.technet.microsoft.com/scriptcenter/site/upload), ya da doğrudan runbook'hello Azure Klasik portalında veya Azure portal hello galerisinden aktarabilirsiniz.

Yalnızca hello Azure Klasik portalında veya Azure portal kullanarak doğrudan hello Runbook'u Galeriden içeri aktarabilirsiniz. Windows PowerShell kullanarak bu işlev gerçekleştiremiyor.

> [!NOTE]
> Hello Runbook Galerisi ' alın ve yükleme ve bir üretim ortamında çalışan çok dikkatli tüm runbook Merhaba içeriğine doğrulamalıdır. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport hello Runbook Galerisi hello Klasik Azure portalı ile runbook
1. İçinde hello Azure Portal'ı tıklatın, **yeni**, **uygulama hizmetleri**, **Otomasyon**, **Runbook**, **Galeri'den**.
2. Bir kategori tooview seçin ilgili runbook'lar ve runbook tooview ayrıntılarını seçin. İstediğiniz hello runbook seçtiğinizde hello sağ ok düğmesine tıklayın.
   
    ![Runbook galerisi](media/automation-runbook-gallery/runbook-gallery.png)
3. Hello runbook Hello içeriğini gözden geçirin ve gereksinimlere hello açıklamasına dikkat edin. İşiniz bittiğinde hello sağ ok düğmesine tıklayın.
4. Merhaba runbook ayrıntılarını girin ve ardından hello onay işareti düğmesine tıklayın. Merhaba runbook adı zaten doldurulur.
5. Merhaba runbook hello üzerinde görünür **Runbook'lar** hello Otomasyon hesabı sekmesi.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport hello Runbook Galerisi hello Azure portalı ile runbook
1. Hello Azure Portal'da, Automation hesabınızı açın.
2. Tıklatın hello üzerinde **Runbook'lar** döşeme tooopen hello listesini.
3. Tıklatın **Gözat galeri** düğmesi.
   
    ![Gözat galeri düğmesi](media/automation-runbook-gallery/browse-gallery-button.png)
4. Bulmak istediğiniz ve tooview seçin hello galeri öğesi ayrıntılarını.
   
    ![Galerisine gözatma](media/automation-runbook-gallery/browse-gallery.png)
5. Tıklayın **görünüm kaynak proje** tooview hello hello öğesinde [TechNet Komut Merkezi](http://gallery.technet.microsoft.com/).
6. bir öğeyi, tooimport üzerinde tıklatın tooview ayrıntılarını ve hello ardından **alma** düğmesi.
   
    ![İçeri Aktar düğmesi](media/automation-runbook-gallery/gallery-item-detail.png)
7. İsteğe bağlı olarak, hello runbook hello adını değiştirin ve ardından **Tamam** tooimport hello runbook.
8. Merhaba runbook hello üzerinde görünür **Runbook'lar** hello Otomasyon hesabı sekmesi.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Bir runbook toohello runbook Galerisi ekleme
Microsoft, tooadd runbook'lar toohello yararlı tooother müşteriler olacağını düşündüğünüz Runbook Galerisi önerir.  Bir runbook tarafından ekleyebilirsiniz [toohello Script Center karşıya](http://gallery.technet.microsoft.com/site/upload) aşağıdaki ayrıntılara hesap hello sürüyor.

* Belirtmeniz gerekir *Windows Azure* hello için **kategori** ve *Otomasyon* hello için **alt kategori** görüntülenen hello runbook toobe için Başlangıç Sihirbazı'nda.  
* Merhaba karşıya yükleme, tek bir .ps1 veya .graphrunbook dosyası olmalıdır.  Merhaba runbook tüm modülleri, alt runbook'ları veya varlıklar gerektiriyorsa, bu hello gönderimi hello açıklaması ve hello runbook hello Açıklamalar bölümüne listelenmelidir.  Birden çok runbook gerektiren bir senaryo varsa, her ayrı olarak yükleyin ve runbook'lar her açıklamalarının listesi hello adlarını hello ilgili. Böylece bunlar hello görünecek aynı etiketleri hello kullandığınızdan emin olun aynı kategori. Bir kullanıcı başka runbook'lar gerekli hello senaryo toowork olduğunu tooread hello açıklama tooknow sahip olur.
* Yayın yapıyorsanız hello etiket "GraphicalPS" ekleme bir **grafik runbook** (olmayan grafik iş akışı). 
* Açıklama hello kullanarak bir PowerShell veya PowerShell iş akışı kod parçacığını eklemek **Ekle kod bölümünde** simgesi.
* Merhaba hello karşıya yükleme özeti hello hello runbook hello işlevselliğini tanımlamak kullanıcı yardımcı olacak ayrıntılı bilgi sağlamalıdır şekilde Runbook Galerisi sonuçları görüntülenir.
* Etiketler toohello karşıya yükleme aşağıdaki Merhaba, bir toothree atamanız gerekir.  Merhaba runbook kendi etiketlerle eşleşecek hello kategoriler altında hello Sihirbazı'nda listelenmez.  Bu listedeki herhangi bir etiket hello Sihirbazı tarafından göz ardı edilir. Eşleşen herhangi bir etiket belirlemezseniz, hello runbook olacaktır hello altında listelenen diğer kategorisi.
  
  * Backup
  * Kapasite Yönetimi
  * Değişiklik denetimi
  * Uyumluluk
  * Geliştirme / Test ortamları
  * Olağanüstü Durum Kurtarma
  * İzleme
  * Düzeltme eki uygulama
  * Sağlama
  * Düzeltme
  * VM yaşam döngüsü yönetimi
* Otomasyon hello galeri saatte bir kez güncelleştirir, böylece katkılarınız hemen göremezsiniz.

## <a name="modules-in-powershell-gallery"></a>PowerShell galerisinde modülleri
PowerShell modülleri larınızda kullanabileceğiniz cmdlet'leri içeren ve Azure Otomasyonu'nda yükleyebilmek için var olan modülleri hello kullanılabilir [PowerShell Galerisi](http://www.powershellgallery.com).  Bu galeriden hello Azure portal'ı başlatın ve doğrudan Azure Automation'a yükleyin veya bunları indirebilir ve bunları el ile yükleyin.  Merhaba modülleri doğrudan hello Klasik Azure Portalı ' yükleyemezsiniz, ancak bunları yükleyebilirsiniz, başka bir modül gibi bunları yükleyin.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport hello Otomasyon modül Galerisine hello Azure portal ile bir modülden
1. Hello Azure Portal'da, Automation hesabınızı açın.
2. Tıklatın hello üzerinde **varlıklar** döşeme tooopen hello varlıkların listesi.
3. Tıklatın hello üzerinde **modülleri** döşeme tooopen hello modüllerin listesini.
4. Tıklatın hello üzerinde **Gözat galeri** düğmesi ve hello Gözat galeri dikey başlatıldığında.
   
    ![Modül Galerisi](media/automation-runbook-gallery/modules-blade.png) <br>
5. Merhaba Gözat galeri dikey başlatıldıktan sonra alanları izleyen hello göre arama yapabilirsiniz:
   
   * Modül adı
   * Etiketler
   * Yazar
   * Cmdlet/DSC kaynağı adı
6. İlgilendiğiniz ve tooview seçin bir modülü bulmak ayrıntılarını.  
   Belirli bir modüle ayrıntıya, bağlantı geri toohello dahil olmak üzere hello modülü hakkında daha fazla bilgi görüntüleyebilirsiniz PowerShell Galerisi, gereken tüm bağımlılıkları ve tüm hello cmdlet'leri ve/veya modülü hello DSC kaynakları içerir.
   
    ![PowerShell modülü ayrıntıları](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. tooinstall hello modüle doğrudan Azure Otomasyonu tıklatın hello **alma** düğmesi.
   
    ![İçeri aktarma modülü düğmesi](media/automation-runbook-gallery/module-import-button.png)
8. Merhaba İçe Aktar düğmesini tıklatın hakkında tooimport olduğunuz hello modül adı görürsünüz. Tüm hello bağımlılıkları yüklediyseniz, hello **Tamam** düğmesi etkin olacaktır. Eksik bağımlılıkları, bu modül içeri aktarmadan önce tooimport olanlar gerekir.
9. Tıklatın **Tamam** tooimport hello modülü ve hello modülü dikey başlayacaktır. Azure Otomasyonu modülü tooyour hesabı aldığında hello modülü ve hello cmdlet'leri hakkındaki meta verileri ayıklar.
   
    ![İçeri aktarma modülü dikey penceresi](media/automation-runbook-gallery/module-import-blade.png)
   
    Her etkinlik ayıklanan toobe gerektiğinden bu birkaç dakika sürebilir.
10. Bir bildirim alacaksınız bu hello modül dağıtılan ve tamamlandıktan sonra bir bildirim.
11. Merhaba modülü içeri aktarıldıktan sonra hello kullanılabilir etkinlikler görür ve runbook'larınızda ve istenen durum yapılandırması kaynaklarını kullanabilirsiniz.

## <a name="requesting-a-runbook-or-module"></a>Bir runbook veya modülü isteme
Çok istekleri göndermek[kullanıcı sesi](https://feedback.azure.com/forums/246290-azure-automation/).  Bir runbook yazma Yardım veya PowerShell hakkında bir sorunuz varsa, bir soru tooour sonrası [Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Sonraki Adımlar
* runbook'ları ile çalışmaya tooget bakın [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md)
* runbook, PowerShell ve PowerShell iş akışı arasında toounderstand hello farkları görmeniz [öğrenme PowerShell iş akışı](automation-powershell-workflow.md)

