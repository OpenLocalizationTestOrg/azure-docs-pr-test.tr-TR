---
title: Orchestrator tooAzure Otomasyon gelen aaaMigrating | Microsoft Docs
description: "Nasıl toomigrate runbook'ları ve tümleştirme paketleri System Center Orchestrator tooAzure Otomasyon açıklar."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Orchestrator tooAzure Otomasyon (Beta) ' geçiş
Runbook'ları [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) Azure automation'daki runbook'lar Windows PowerShell tabanlı, özellikle Orchestrator için yazılmış tümleştirme paketleri etkinliklerden dayanır.  [Grafik runbook'lar](automation-runbook-types.md#graphical-runbooks) Azure Otomasyonu'nda PowerShell cmdlet'leri, alt runbook'ları ve varlıkları temsil eden etkinliklerini ile benzer bir görünüm tooOrchestrator runbook'lar sahip.

Merhaba [System Center Orchestrator geçiş Araç Seti](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) araçları tooassist içerir, Orchestrator tooAzure Otomasyon runbook'ları dönüştürme içinde.  Ayrıca tooconverting hello runbook kendilerini hello tümleştirme paketleri hello runbook'ları Windows PowerShell cmdlet'leri ile toointegration modülleri kullanmanızı hello etkinliklerle dönüştürmeniz gerekir.  

Aşağıdaki hello temel Orchestrator runbook'ları tooAzure Otomasyon dönüştürme işlemidir.  Bu adımların her biri aşağıdaki hello bölümlerde ayrıntılı olarak açıklanmıştır.

1. Merhaba karşıdan [System Center Orchestrator geçiş Araç Seti](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) hello araçları ve bu makalede açıklanan modüllerini içerir.
2. İçeri aktarma [standart etkinlikler modül](#standard-activities-module) Azure Otomasyonu içine.  Bu, dönüştürülmüş runbook'lar tarafından kullanılan standart Orchestrator etkinlikleri dönüştürülen sürümlerini içerir.
3. İçeri aktarma [System Center Orchestrator tümleştirme modülleri](#system-center-orchestrator-integration-modules) System Center erişim, runbook'lar tarafından kullanılan bu tümleştirme paketleri için Azure Automation içine.
4. Hello kullanarak özel ve üçüncü taraf tümleştirme paketleri dönüştürmek [tümleştirme paketi dönüştürücü](#integration-pack-converter) ve Azure Automation'a içeri aktarın.
5. Hello kullanarak Orchestrator runbook'ları Dönüştür [Runbook dönüştürücü](#runbook-converter) ve Azure Otomasyonu'nda yükleyin.
6. El ile Merhaba Runbook dönüştürücü bu kaynakları dönüştürmez beri Azure Otomasyonu'nda gerekli Orchestrator varlıklar oluşturun.
7. Yapılandırma bir [karma Runbook çalışanı](#hybrid-runbook-worker) runbook'lardaki yerel kaynaklara erişecek, yerel veri merkezi toorun dönüştürülür.

## <a name="service-management-automation"></a>Hizmet Yönetim Otomasyonu
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) depolar ve Orchestrator gibi yerel veri merkezinizdeki runbook'ları çalıştıran ve hello kullandığı aynı tümleştirme modülleri Azure Otomasyonu olarak. Merhaba [Runbook dönüştürücü](#runbook-converter) Orchestrator runbook'ları toographical runbook'ları, ancak SMA'da desteklenmez dönüştürür.  Merhaba yüklemeye devam edebilirsiniz [standart etkinlikler modül](#standard-activities-module) ve [System Center Orchestrator tümleştirme modülleri](#system-center-orchestrator-integration-modules) SMA, içine ancak el ile [runbook'larınızı yeniden](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>Karma Runbook Çalışanı
Orchestrator runbook'ları bir veritabanı sunucusunda depolanan ve runbook sunucuları, hem de yerel veri merkezinizde çalıştırın.  Azure Otomasyonu runbook'ları hello Azure bulut depolanır ve yerel veri merkezi kullanarak çalıştırabilirsiniz bir [karma Runbook çalışanı](automation-hybrid-runbook-worker.md).  Orchestrator'ı yerel sunucularda tasarlanmış toorun olduğundan dönüştürülen runbook'ları genellikle nasıl çalışacağını budur.

## <a name="integration-pack-converter"></a>Tümleştirme paketi dönüştürücü
Merhaba tümleştirme paketi dönüştürücü dönüştürür hello kullanılarak oluşturulan tümleştirme paketleri [Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration modülleri tabanlı Azure Automation'a içeri aktarılabilir Windows PowerShell veya Hizmet Yönetimi Otomasyonu.  

Merhaba tümleştirme paketi dönüştürücü çalıştırdığınızda, tooselect bir tümleştirme paketi (.oıp) dosyası sağlayacak bir sihirbaz ile sunulur.  Hello sihirbazını sonra bu tümleştirme paketinde hello etkinlikleri listeler ve geçirilecek tooselect sağlar.  Merhaba Sihirbazı tamamladığınızda, her hello özgün Integration pack Merhaba etkinlikler için karşılık gelen bir cmdlet'i içeren bir tümleştirme modülü oluşturur.

### <a name="parameters"></a>Parametreler
Herhangi bir etkinlikte hello tümleştirme paketi hello karşılık gelen cmdlet'inin hello tümleştirme modülü dönüştürülmüş tooparameters özellikleridir.  Windows PowerShell cmdlet'leri sahip bir dizi [ortak parametreler](http://technet.microsoft.com/library/hh847884.aspx) tüm cmdlet'ler ile kullanılabilir.  Örneğin, hello - Verbose parametresi bir cmdlet neden toooutput ayrıntılı çalışmasıyla ilgili bilgileri.  Hiçbir cmdlet'i aynı ortak parametre olarak ad hello parametresiyle olabilir.  Aktivite ortak parametre olarak aynı ad hello sahip bir özellik varsa, bu hello sihirbaz hello parametresi için başka bir ad, tooprovide sorar.

### <a name="monitor-activities"></a>İzleme etkinlikleri
İzleme Orchestrator başlangıç ile runbook'ları bir [etkinliğini İzle](http://technet.microsoft.com/library/hh403827.aspx) ve sürekli olarak belirli bir olay tarafından çağrılan bekleme toobe çalıştırın.  İzleyici etkinlikler hello tümleştirme paketindeki dönüştürülmeyecek şekilde azure Otomasyonu İzleyici runbook'ları desteklemez.  Bunun yerine, bir yer tutucu cmdlet hello tümleştirme modülü hello monitör etkinliği için oluşturulur.  Bu cmdlet herhangi bir işlevselliğe sahiptir, ancak yüklü toobe kullanan herhangi bir dönüştürülmüş runbook sağlar.  Bu runbook, Azure automation'da mümkün toorun olmaz ancak değiştirmenize olanak sağlayan yüklenebilir.

### <a name="integration-packs-that-cannot-be-converted"></a>Dönüştürülemiyor tümleştirme paketleri
OIT ile oluşturulmayan tümleştirme paketleri hello tümleştirme paketi dönüştürücü ile dönüştürülemiyor. Bu aracı ile şu anda dönüştürülemez Microsoft tarafından sağlanan bazı tümleştirme paketleri de vardır.  Dönüştürülen bu tümleştirme paketleri sürümleri olmuştur [indirme için sağlanan](#system-center-orchestrator-integration-modules) böylece Azure Otomasyonu veya Service Management Automation yüklenebilir.

## <a name="standard-activities-module"></a>Standart etkinlikler Modülü
Orchestrator içeren bir dizi [standart etkinlikler](http://technet.microsoft.com/library/hh403832.aspx) bir tümleştirme paketinde bulunmayan ancak birçok runbook'lar tarafından kullanılır.  Bu etkinliklerin her biri için eşdeğer bir cmdlet'i içeren bir tümleştirme modülü Hello standart etkinlikler modülüdür.  Standart etkinlik kullanan dönüştürülmüş runbook'ları içe aktarmadan önce Azure Otomasyonu'nda Bu tümleştirme modülü yüklemeniz gerekir.

Ayrıca toosupporting runbook'lar dönüştürülür, Orchestrator toobuild yeni runbook'ları Azure Automation aşina birisi tarafından hello standart etkinlikler modülündeki hello cmdlet'leri kullanılabilir.  Tüm hello standart etkinlikler Hello işlevselliğini cmdlet'leriyle gerçekleştirilebilir, ancak bunlar farklı çalışabilir.  kendi ilgili etkinlikler ve kullanım aynı parametreleri hello gibi hello dönüştürülen hello standart etkinlikler modül çalışacak cmdlet'leri aynı hello.  Bu hello var olan Orchestrator runbook Yazar kendi geçiş tooAzure Otomasyon runbook'ları için yardımcı olabilir.

## <a name="system-center-orchestrator-integration-modules"></a>System Center Orchestrator tümleştirme modülleri
Microsoft sağlar [tümleştirme paketleri](http://technet.microsoft.com/library/hh295851.aspx) runbook'lar tooautomate System Center bileşenleri ve diğer ürünler oluşturmak için.  Bu tümleştirme paketleri bazıları OIT üzerinde şu anda bağlı ancak dönüştürülen toointegration modülleri bilinen sorunları nedeniyle şu anda olamaz.  [System Center Orchestrator tümleştirme modülleri](https://www.microsoft.com/download/details.aspx?id=49555) Azure Automation ve Service Management Automation aktarılabilen Bu tümleştirme paketleri dönüştürülen sürümlerini içerir.  

Merhaba RTM sürümü bu aracı tarafından tümleştirme paketi dönüştürücü yayımlanan hello ile dönüştürülebilir OIT göre hello tümleştirme paketleri sürümleri güncelleştirildi.  Yönergeler de size hello tümleştirme paketleri etkinliklerden kullanmayan runbook'ları dönüştürme OIT üzerinde temel tooassist sağlanacaktır.

## <a name="runbook-converter"></a>Runbook dönüştürücü
Merhaba Runbook dönüştürücü dönüştürür Orchestrator runbook'larınızda [grafik runbook'lar](automation-runbook-types.md#graphical-runbooks) Azure Automation'a alınabilir.  

Runbook dönüştürücü adlı bir cmdlet ile bir PowerShell modülü olarak uygulanan **ConvertFrom SCORunbook** hello dönüştürme gerçekleştirir.  Merhaba aracı yüklediğinizde, hello cmdlet yükleyen bir kısayol tooa PowerShell oturumu oluşturur.   

Aşağıdaki hello temel işlem tooconvert Orchestrator runbook'u ve Azure Automation'a aktarabilir.  Merhaba aşağıdaki bölümlerde daha ayrıntılı bilgi hello aracını kullanarak ve dönüştürülen runbook'larla çalışma sağlar.

1. Bir veya daha fazla çalışma kitabı Orchestrator'ı verin.
2. Merhaba runbook'taki tüm etkinlikler için tümleştirme modülleri alın.
3. Merhaba Orchestrator runbook'ları hello dışarı aktarılan dosyayı dönüştürün.
4. Günlükleri toovalidate hello dönüştürme ve toodetermine bilgileri tüm gerekli el ile gerçekleştirilen görevleri gözden geçirin.
5. Dönüştürülen runbook'ları Azure Automation'a aktarabilir.
6. Gerekli tüm varlıkları Azure Otomasyonu'nda oluşturun.
7. Azure Otomasyonu toomodify Hello runbook'ta gerekli tüm etkinlikleri düzenleyin.

### <a name="using-runbook-converter"></a>Runbook dönüştürücü kullanma
Merhaba sözdizimi **ConvertFrom SCORunbook** aşağıdaki gibidir:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* Yol toohello verme RunbookPath - içeren hello runbook'lar tooconvert dosya.
* Modül - hello runbook'lar etkinlikler içeren tümleştirme modülleri listesini virgülle ayrılmış.
* OutputFolder - yol toohello klasörü toocreate grafik runbook'lar dönüştürülür.

Aşağıdaki örnek komut dönüştürür hello olarak adlandırılan dışa aktarma dosyası runbook'larda hello **MyRunbooks.ois_export**.  Bu runbook'lar hello Active Directory ve Data Protection Manager tümleştirme paketlerini kullanın.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Günlük dosyaları
Merhaba Runbook dönüştürücü hello günlük dosyalarında aşağıdaki hello oluşturacak hello aynı konumda runbook dönüştürülür.  Merhaba dosyaları zaten mevcutsa, ardından bunlar hello son dönüştürme bilgileriyle üzerine yazılır.

| Dosya | İçindekiler |
|:--- |:--- |
| Runbook dönüştürücü - Progress.log |Ayrıntılı adımlar başarıyla dönüştürülen her etkinlik için bilgi ve uyarı dönüştürülmez her etkinlik için de dahil olmak üzere hello dönüştürme. |
| Runbook dönüştürücü - Summary.log |Merhaba özetini dönüştürme tüm uyarılar dahil olmak üzere en son ve dönüştürülen hello runbook için gerekli bir değişken oluşturma gibi tooperform gereken görevleri izleyin. |

### <a name="exporting-runbooks-from-orchestrator"></a>Orchestrator'ı runbook'ları dışarı aktarma
runbook'ları bir veya daha fazla Orchestrator dışa aktarma dosyasından Hello Runbook dönüştürücü çalışır.  Merhaba dışa aktarma dosyasında her Orchestrator runbook için karşılık gelen bir Azure Otomasyonu runbook'u oluşturur.  

tooexport Orchestrator, bir runbook'tan Runbook Designer'da hello runbook hello adını sağ tıklatın ve seçin **verme**.  tooexport bir klasördeki tüm runbook'lar sağ hello hello klasörün adını ve select **verme**.

### <a name="runbook-activities"></a>Runbook etkinlikleri
Merhaba Runbook dönüştürücü hello Orchestrator runbook tooa karşılık gelen etkinlik Azure Automation her bir etkinlik dönüştürür.  Dönüştürülemez bu etkinlikler için uyarı metni ile Merhaba runbook'taki bir yer tutucu etkinlik oluşturulur.  Azure Automation'a dönüştürülen hello runbook içe aktardıktan sonra bu etkinlikler hiçbirini gerekli hello işlevleri gerçekleştirmek geçerli etkinlikleri ile değiştirmeniz gerekir.

Tüm Orchestrator etkinlikleri hello [standart etkinlikler modül](#standard-activities-module) dönüştürülür.  Bu modülde ancak olmayan ve dönüştürülmez bazı standart Orchestrator etkinlikleri vardır.  Örneğin, **Platform olayı Gönder** hello olay belirli tooOrchestrator olduğundan Azure Otomasyonu eşdeğeri vardır.

[İzleme etkinlikleri](https://technet.microsoft.com/library/hh403827.aspx) Azure Otomasyonu'nda hiçbir eşdeğer toothem olduğundan dönüştürülmez.  Merhaba istisnadır izleme etkinlikleri [dönüştürülen tümleştirme paketleri](#integration-pack-converter) dönüştürülmüş toohello yer tutucu etkinlik olacaktır.

Herhangi bir etkinlikten bir [dönüştürülen tümleştirme paketi](#integration-pack-converter) hello yolu toohello tümleştirme modülü ile Merhaba sağlarsanız, dönüştürülecek **modülleri** parametresi.  System Center tümleştirme paketleri için hello kullanabilirsiniz [System Center Orchestrator tümleştirme modülleri](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Orchestrator kaynakları
Merhaba Runbook dönüştürücü, runbook'ları, diğer Orchestrator kaynakları sayaçları, değişkenleri veya bağlantıları gibi değil yalnızca dönüştürür.  Sayaçlar, Azure Automation'da desteklenmez.  Değişkenleri ve bağlantıları desteklenir, ancak el ile oluşturmanız gerekir.  Hello günlük dosyalarını hello runbook gibi kaynakları gerektiriyorsa bildirir ve Azure Automation toocreate Merhaba ihtiyacınız ilgili kaynakları runbook toooperate düzgün dönüştürülen belirtin.

Örneğin, bir runbook bir etkinlik değişken toopopulate belirli bir değeri kullanabilir.  Merhaba dönüştürülmüş runbook hello etkinlik dönüştürün ve hello hello Orchestrator değişken olarak aynı ad ile Azure Otomasyonu değişken varlığı belirtin.  Bu hello Not edilir **Runbook dönüştürücü - Summary.log** hello dönüştürmeden sonra oluşturulan dosyası.  İhtiyacınız olacak toomanually oluşturma bu değişken varlığı Azure Otomasyonu'nda hello runbook kullanmadan önce.

### <a name="input-parameters"></a>Giriş parametreleri
Orchestrator runbook'ları kabul hello giriş parametreleriyle **verileri Başlat** etkinlik.  Merhaba runbook dönüştürülmekte olan bu etkinliği içeriyorsa, sonra bir [giriş parametresi](automation-graphical-authoring-intro.md#runbook-input-and-output) hello Azure Otomasyonu runbook hello etkinliğinde her parametre için oluşturulur.  A [iş akışı betiği denetim](automation-graphical-authoring-intro.md#activities) etkinlik alır ve her bir parametreyi döndüren dönüştürülen hello runbook'ta oluşturulur.  Giriş parametresi kullanan tüm etkinlikleri hello runbook'taki toohello çıkış bu etkinliğinden bakın.

Bu strateji kullanılır hello toobest yansıtma hello hello Orchestrator runbook işlevindeki nedenidir.  Yeni grafik runbook'lar etkinlikler Runbook giriş veri kaynağı kullanarak tooinput parametrelerini doğrudan başvurmalıdır.

### <a name="invoke-runbook-activity"></a>Runbook'u Çağır etkinliğine
Orchestrator runbook'ları başlatmak diğer runbook'ları ile Merhaba **Runbook'u Çağır** etkinlik. Merhaba runbook dönüştürülmekte olan bu etkinliği ve hello içerip içermediğini **tamamlanması bekle** seçeneği ayarlanmış sonra runbook etkinliği dönüştürülen hello runbook'ta oluşturulur.  Merhaba, **tamamlanması bekle** seçeneği ayarlı değil, sonra kullanan bir iş akışı betiği etkinlik oluşturulur **başlangıç AzureAutomationRunbook** toostart hello runbook.  Azure Automation'a dönüştürülen hello runbook içeri aktardıktan sonra hello etkinliğinde belirtilen hello bilgilerle bu etkinliği değiştirmeniz gerekir.

## <a name="related-articles"></a>İlgili makaleler
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Hizmet Yönetimi Otomasyonu](https://technet.microsoft.com/library/dn469260.aspx)
* [Karma Runbook çalışanı](automation-hybrid-runbook-worker.md)
* [Orchestrator standart etkinlikler](http://technet.microsoft.com/library/hh403832.aspx)
* [İndirme System Center Orchestrator geçiş Araç Seti](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
