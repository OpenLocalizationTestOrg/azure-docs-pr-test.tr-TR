---
title: aaaWhat olan Azure Otomasyonu | Microsoft Docs
description: "Azure Automation'ın sağladığı değerleri öğrenin ve oluşturma, runbook'ları ve Azure Automation DSC kullanmaya başlamanıza böylece toocommon soruları yanıtlar alın."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "otomasyon nedir, azure otomasyonu, azure otomasyonu örnekleri"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Azure Automation’a genel bakış
Microsoft Azure Otomasyonu, Bulut ve Kurumsal ortamda sık gerçekleştirilen hello el ile uzun süreli, hatasız ve sık tekrarlanan görevleri kullanıcılar tooautomate için bir yol sağlar. Kaydeder zaman hello normal yönetim görevlerinin güvenilirliğini artırır ve hatta bunları toobe otomatik olarak zamanlar düzenli aralıklarla gerçekleştirilen. Runbook’ları kullanarak işlemleri otomatik hale getirebilir ya da İstenen Durum Yapılandırması’nı kullanarak yapılandırmayı otomatik hale getirebilirsiniz. Bu makale, Azure Automation’a ilişkin kısa bir genel bakış sağlar ve bazı sık sorulan soruları yanıtlar. Hello farklı konuları hakkında daha ayrıntılı bilgi için bu kitaplıktaki tooother makaleleri başvurabilir.

## <a name="automating-processes-with-runbooks"></a>Runbook'larla işlemleri otomatik hale getirme
Bir runbook, Azure Automation’da bazı otomatik işlemleri gerçekleştiren görevler grubudur. Bir sanal makineyi başlatma ve günlük girişi oluşturma gibi basit bir işlem olabilir veya diğer küçük runbook'ları tooperform karmaşık bir işlem birden fazla kaynak veya hatta birden çok Bulut ve şirket içi ortamları arasında birleştiren karmaşık bir runbook'unuz olabilir.  

Örneğin, bir SQL veritabanı toohello veritabanına bağlanma bağlanan toohello sunucusu gibi birden fazla adımı içeren maksimum boyuta yaklaşıyorsa kesilmesi için işlem, hello veritabanının mevcut boyutunu alma, olup olmadığını denetleyin var olan bir el ile olabilir eşiği aştı ve ardından kesme ve kullanıcıyı bilgilendirir. Bu adımların her birini el ile gerçekleştirmek yerine, tüm bu adımları tek bir işlem olarak gerçekleştirecek bir runbook oluşturabilirsiniz. Merhaba runbook'u başlatmak, hello SQL server adı, veritabanı adı ve alıcı e-posta gibi hello gerekli bilgileri sağlayın ve geri hello İşlem tamamlanırken arkanıza yaslanırsınız. 

## <a name="what-can-runbooks-automate"></a>Runbook’lar neleri otomatik hale getirir?
Azure Automation’daki runbook’lar Windows PowerShell ya da Windows PowerShell İş Akışı tabanlıdır, bu nedenle bunlar PowerShell’in yapabileceği her şeyi yapar. Bir uygulama veya hizmetin API’si varsa, bir runbook bununla çalışabilir. Merhaba uygulaması için bir PowerShell modülü sahip bu modülü Azure Automation'a yükleyebilir ve bu cmdlet'leri runbook'unuza ekleyebilirsiniz. Azure Otomasyonu runbook'ları Azure bulut hello çalıştırın ve herhangi bir bulut kaynaklarına veya hello buluttan erişilebilen dış kaynaklara erişebilir. Kullanarak [karma Runbook çalışanı](automation-hybrid-runbook-worker.md), runbook'lar yerel verilerinizi merkezi toomanage yerel kaynakları çalıştırabilirsiniz. 

## <a name="getting-runbooks-from-hello-community"></a>Merhaba topluluktan runbook'ları alma
Merhaba [Runbook Galerisi](automation-runbook-gallery.md#runbooks-in-runbook-gallery) değişmeden ortamınızda kullanabilir Microsoft ve hello topluluktan runbook'ları içeren ya da kendi amaçlarınız doğrultusunda özelleştirin. Ayrıca yararlı tooas başvuruları toolearn nasıl oldukları toocreate kendi runbook'ları. Hatta diğer kullanıcıların faydalı bulabileceğini düşündüğünüz kendi runbook'ları toohello galeri katkıda bulunabilir. 

## <a name="creating-runbooks-with-azure-automation"></a>Azure Automation ile Runbook’ları oluşturma
Yapabilecekleriniz [kendi runbook](automation-creating-importing-runbook.md) gelen karalama veya hello runbook'lardan değiştirmek [Runbook Galerisi](http://msdn.microsoft.com/library/azure/dn781422.aspx) da kendi gereksinimleriniz doğrultusunda. Gereksinimlerinize ve PowerShell deneyiminize göre seçebileceğiniz dört farklı [runbook türü](automation-runbook-types.md) vardır. Merhaba PowerShell kodu ile doğrudan toowork tercih sonra kullanabileceğiniz bir [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) veya [PowerShell iş akışı runbook'u](automation-runbook-types.md#powershell-workflow-runbooks) çevrimdışı veya hello Düzenle [metin düzenleyicisini](http://msdn.microsoft.com/library/azure/dn879137.aspx) hello Azure Portalı'nda. Tooedit tercih ederseniz, arka plandaki kod toohello olmaksızın bir runbook'u kullanıma sonra oluşturabileceğiniz bir [grafik runbook](automation-runbook-types.md#graphical-runbooks) hello kullanarak [grafik Düzenleyicisi](automation-graphical-authoring-intro.md) hello Azure Portalı'nda. 

Tooreading izlemeyi mi tercih ediyorsunuz? Aşağıdaki videoya Mayıs 2015 Microsoft Ignite oturumundan hello göz vardır. Not: hello kavramları ve özellikler bu videoda ele alınan bu videonun kaydedilmesinden sonra Azure Otomasyonu değişmiştir doğru olsa da, onu artık hello Azure portal ve destekleyen ek yetenekler daha geniş bir kullanıcı Arabirimine sahiptir.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>İstenen Durum Yapılandırması ile yapılandırma yönetimini otomatik hale getirme
[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) toomanage, sağlayan bir yönetim platformudur dağıtmak ve fiziksel ana bilgisayarlar ve bildirim temelli bir PowerShell söz dizimi kullanarak sanal makineleri yapılandırma zorlayın. Merkezi bir DSC Çekme Sunucusu’nda hedef makinelerin otomatik olarak alabileceği ve uygulayabileceği yapılandırmaları tanımlayabilirsiniz. DSC toomanage yapılandırmaları ve kaynakları kullanabilirsiniz PowerShell cmdlet'leri kümesi sağlar.  

[Azure Automation DSC](automation-dsc-overview.md), PowerShell DSC’ye yönelik kurumsal ortamlar için hizmetler için gerekli hizmetleri sağlayan bulut tabanlı bir çözümdür.  Azure Automation DSC kaynaklarınızı yönetebilir ve yapılandırmaları toovirtual ya da bir DSC çekme sunucusunda hello Azure bulut almak fiziksel makineleri uygulayın.  Bu ayrıca, düğümlerin kendilerine atanan yapılandırmalardan sapması ve yeni bir yapılandırma uygulanması gibi önemli olayları size bildiren raporlama hizmetleri de sağlar. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Azure Automation’da kendi DSC yapılandırmalarınızı oluşturma
[DSC yapılandırmaları](automation-dsc-overview.md) hello istenen düğüm durumunu belirtin.  Birden çok düğüm uygulayabilirsiniz hello tümünün aynı durumu yapılandırmayı aynı yapılandırma tooassure.  Yerel makinenizde bir metin düzenleyicisi kullanarak yapılandırma oluşturabilir ve ardından bunu derleyebileceğiniz ve düğümlerini uygulayabileceğiniz Azure Automation’a aktarabilirsiniz.

## <a name="getting-modules-and-configurations"></a>Modülleri ve yapılandırmaları alma
Alma [PowerShell modülleri](automation-runbook-gallery.md#modules-in-powershell-gallery) runbook'larınızda ve DSC kaynaklarından hello kullanabileceğiniz cmdlet'leri içeren [PowerShell Galerisi](http://www.powershellgallery.com/). Hello Azure portal bu Galeriden başlatın ve modülleri doğrudan Azure Automation'a aktarabilir ya da indirebilir ve bunları el ile içeri aktarın. Merhaba modülleri doğrudan hello Azure Portalı ' yükleyemezsiniz, ancak bunları yükleyebilirsiniz, başka bir modül gibi bunları yükleyin. 

## <a name="example-practical-applications-of-azure-automation"></a>Azure Automation’ın örnek pratik uygulamalar
Aşağıda Azure Automation Otomasyon senaryosu hello türleri nelerdir, yalnızca birkaç örnek verilmiştir. 

* Farklı Azure aboneliklerinde sanal makineler oluşturun ve kopyalayın. 
* Dosya kopyalarını yerel makine tooan Azure Blob Storage kapsayıcısına zamanlayın. 
* Bir hizmet reddi saldırısı algılandığında,istekleri reddetme gibi güvenlik işlevlerini otomatik hale getirin. 
* Makinelerin yapılandırılmış güvenlik ilkesiyle sürekli hizalanmasını sağlayın.
* Uygulana kodunun buluta ve şirket içi altyapıya sürekli dağıtımını yönetin. 
* Azure’da laboratuvar ortamınız için bir Active Directory ormanı oluşturun. 
* DB en büyük boyuta yaklaşıyorsa, SQL veritabanındaki bir tabloyu kesin. 
* Bir Azure Web sitesi için ortam ayarlarını uzaktan güncelleştirin. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Azure Otomasyonu tooother Otomasyon araçları nasıl ilişkilidir?
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) hello özel bulutta yönetim görevlerini hedeflenen tooautomate değil. [Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/) bileşeni olarak veri merkezinize yerel olarak yüklenir. SMA ve Azure Otomasyonu kullanmak hello aynı runbook biçimini temel Windows PowerShell ve Windows PowerShell iş akışı, ancak SMA desteklemiyor [grafik runbook'lar](automation-graphical-authoring-intro.md).  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) şirket içi kaynakların otomasyonuna yöneliktir. Azure Automation ve Service Management Automation farklı runbook biçimini kullanır ve betiklere gerek kalmadan bir grafik arabirim toocreate runbook'ları vardır. Runbook'ları, Tümleştirme Paketleri’nde bulunan özellikle Orchestrator için yazılmış olan etkinliklerden oluşur. 

## <a name="where-can-i-get-more-information"></a>Daha fazla bilgiyi nereden bulabilirim?
Çeşitli kaynaklar, toolearn Azure Automation ve kendi runbook'larınızı oluşturma hakkında daha fazla bilgi için kullanılabilir. 

* **Azure Automation Kitaplığı** şu anda bulunduğunuz yerdir. Bu kitaplıktaki Hello makaleler hello yapılandırma ve yönetim Azure Automation ve kendi runbook'ları yazma için kapsamlı belgeler sağlar. 
* [Azure PowerShell cmdlet'leri](http://msdn.microsoft.com/library/jj156055.aspx) Windows PowerShell kullanarak Azure işlemlerini otomatik hale getirme hakkında bilgi sağlar. Runbook'ları Azure kaynakları ile bu cmdlet'leri toowork kullanın. 
* [Yönetim Web günlüğü](https://azure.microsoft.com/blog/tag/azure-automation/) Microsoft'tan Azure Automation ve diğer yönetim teknolojilerine hello en son bilgileri sağlar. Toothis blog toostay hello ile toodate yukarı son hello Azure Automation ekibinin abone olmalıdır. 
* [Automation Forumu](http://go.microsoft.com/fwlink/p/?LinkId=390561) Microsoft ve hello Automation topluluk tarafından ele Azure Otomasyonu toobe hakkında toopost sorular sağlar. 
* [Azure Automation Cmdlet'leri](https://msdn.microsoft.com/library/mt244122.aspx) yönetim görevlerini otomatik hale getirmek için bilgiler sağlar. Bu cmdlet toomanage Automation hesaplarını, varlıkları, runbook'ları, DSC içerir.

## <a name="can-i-provide-feedback"></a>Geribildirim sağlayabilir miyim?
**Lütfen bize geri bildirimde bulunun.** Bir Azure Automation runbook çözümü veya bir tümleştirme modülü arıyorsanız, Betik Merkezi'ne bir Betik İsteği gönderin. Azure Automation ile ilgili geribildirim ya da özellik isteğiniz varsa, [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback)’da yayınlayın. Teşekkür ederiz! 

