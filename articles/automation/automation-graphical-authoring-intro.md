---
title: "aaaGraphical Azure Otomasyonu'nda geliştirme | Microsoft Docs"
description: "Grafik yazma toocreate runbook'lar için Azure Automation kodu ile çalışma olmadan sağlar. Bu makalede bir giriş toographical yazma sağlar ve tüm hello ayrıntıları grafik runbook oluşturma toostart gerekli."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Grafik Azure Otomasyonu'nda yazma
## <a name="introduction"></a>Giriş
Grafik yazma toocreate runbook'ları hello temel Windows PowerShell veya PowerShell iş akışı kodu hello karmaşıklığını Azure Otomasyon için sağlar. Cmdlet'ler ve runbook'ları kitaplıktan etkinlikleri toohello tuvale Ekle, birbirine bağlamak ve tooform bir iş akışı yapılandırın.  System Center Orchestrator veya Service Management Automation (SMA) ile herhangi bir zamanda çalıştıysanız, bu tanıdık tooyou görünmelidir.   

Bu makalede bir giriş toographical grafik runbook oluşturmaya başlamanızı tooget ihtiyacınız yazma ve hello kavramları sağlar.

## <a name="graphical-runbooks"></a>Grafik runbook'lar
Azure Otomasyonu'nda tüm runbook'lar Windows PowerShell iş akışlarıdır.  Grafik ve grafik PowerShell iş akışı runbook'ları hello Otomasyon çalışanları tarafından çalıştırılan PowerShell kodu oluşturur, ancak mümkün tooview değildir, veya doğrudan değiştirebilirsiniz.  Bir grafik runbook dönüştürülmüş tooa grafik PowerShell iş akışı runbook'u ve tam tersini olabilir, ancak dönüştürülen tooa metin biçiminde runbook olamaz. Var olan bir metinsel runbook'un hello grafik Düzenleyicisi aktarılamaz.  

## <a name="overview-of-graphical-editor"></a>Grafik Düzenleyicisi'ne genel bakış
Oluşturma veya grafik runbook düzenleme hello Azure portal hello grafik Düzenleyicisi açabilirsiniz.

![Grafik çalışma](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

Merhaba aşağıdaki bölümlerde hello grafik Düzenleyicisi'nde hello denetimleri açıklanmaktadır.

### <a name="canvas"></a>Tuvale
Merhaba tuvale runbook'unuz tasarım burada ' dir.  Hello düğümlerinden hello kitaplığı denetim toohello runbook'taki etkinlikler ekleme ve bunları Itanium tabanlı sistemler için bağlantılar toodefine hello mantığı hello runbook'un ile bağlayın.

Hello tuvale toozoom hello altındaki içeri ve dışarı hello denetimleri kullanabilirsiniz.

![Grafik çalışma](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>Kitaplığı denetimi
Merhaba kitaplığı denetimi seçildiği yer [etkinlikleri](#activities) tooadd tooyour runbook.  Bunları, bunları tooother etkinlikleri eriştikleri toohello tuvale ekleyin.  Aşağıdaki tablonun hello açıklanan dört bölüm içerir.

| Bölüm | Açıklama |
|:--- |:--- |
| Cmdlet'leri |Kullanılabilir tüm hello cmdlet'leri runbook'unuza içerir.  Cmdlet modülü tarafından düzenlenir.  Tüm otomasyon hesabınızda yüklediğiniz hello modülleri kullanılabilir. |
| Runbook'lar |Merhaba runbook Otomasyon hesabınızda içerir. Bu runbook'lar alt runbook'lar olarak kullanılan toohello tuvale toobe eklenebilir. Aynı tür düzenlenmekte olan runbook hello gibi çekirdek Merhaba, yalnızca runbook'lar gösterilir; Grafik PowerShell iş akışı runbook'ları yalnızca PowerShell iş akışı tabanlı runbook'ları gösterilmese için grafik runbook'ları yalnızca PowerShell tabanlı runbook'lar gösterilir. |
| Varlıklar |Merhaba içeren [Otomasyon varlıkları](http://msdn.microsoft.com/library/dn939988.aspx) Otomasyon hesabınızda runbook'unuzda kullanılabilir.  Bir varlık tooa runbook eklediğinizde, hello seçili varlığı alır bir iş akışı etkinliği ekleyeceksiniz.  Değişken varlıkları Hello durumda seçtiğiniz tooadd bir etkinlik tooget değişken veya ayarlı hello değişkeni hello olup olmadığını. |
| Runbook denetimi |Kullanılabilir runbook denetimi etkinlikleri geçerli runbook'unuzda içerir. A *birleşim* birden çok girişi alır ve tüm önce devam ediliyor hello iş akışı tamamlanana kadar bekler. A *kod* etkinlik bir veya daha fazla kod satırı bulunmaktadır PowerShell veya PowerShell iş akışı hello grafik runbook türüne bağlı olarak çalışır.  Bu etkinlik için özel kod veya diğer etkinliklerle zor tooachieve işlevselliği için kullanabilirsiniz. |

### <a name="configuration-control"></a>Yapılandırma denetimi
Merhaba yapılandırma denetimi ayrıntıları hello tuvalde seçili bir nesne için verdiğiniz ' dir. Bu denetimde kullanılabilir Hello özellikleri hello seçilen nesne türüne bağlıdır.  Merhaba yapılandırma denetimi bir seçeneği belirlediğinizde, sipariş tooprovide ek bilgileri ek dikey pencere açılır.

### <a name="test-control"></a>Test denetimi
Merhaba grafik Düzenleyicisi'ni ilk başlattığınızda hello Test denetimi görüntülenmez. Ne zaman açıldığında, etkileşimli olarak [bir grafik runbook'u test](#graphical-runbook-procedures).  

## <a name="graphical-runbook-procedures"></a>Grafik runbook yordamları
### <a name="exporting-and-importing-a-graphical-runbook"></a>Bir grafik runbook alma ve verme
Yalnızca bir grafik runbook yayımlanan sürümüne hello dışarı aktarabilirsiniz.  Merhaba runbook henüz yayımlanmadı, ardından hello **yayımlanan verme** düğmesi devre dışı bırakılacak.  Merhaba tıkladığınızda **yayımlanan verme** düğmesini tıklatın, hello runbook indirilen tooyour yerel bilgisayardır.  Merhaba dosyasının Hello adı ile Merhaba runbook'un hello adı ile eşleşen bir *graphrunbook* uzantısı.

![Yayımlanan dışarı aktarma](media/automation-graphical-authoring-intro/runbook-export.png)

Merhaba seçerek bir grafik veya grafik PowerShell iş akışı runbook dosyasını da içeri aktarabilirsiniz **alma** bir runbook eklerken seçeneği.   Merhaba dosya tooimport seçtiğinizde tutabilirsiniz aynı hello **adı** veya yeni bir tane girin.  Seçili hello dosya ve tooselect olası çakışmaları vardır ve dönüştürme sırasında olabilir bir ileti sunulur doğru değilse farklı bir tür çalışırsanız, değerlendirir sonra hello Runbook türü alan runbook hello türünü görüntüler sözdizimi hataları.  

![Runbook'u İçeri Aktar](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>Grafik runbook'u test etme
Merhaba bırakarak sürümü değiştirmeden hello runbook'un yayımlanan ya da onu yayımlamadan önce yeni bir runbook test edebilirsiniz hello Azure portal hello bir runbook'un taslak sürümünü test edebilirsiniz. Bu, runbook hello tooverify hello yayımlanan sürümü değiştirmeden önce düzgün çalışmasını sağlar. Bir runbook'u test ettiğinizde hello taslak runbook yürütülür ve gerçekleştirdiği tüm işlemler tamamlanır. İş Geçmişi oluşturulmaz, ancak çıktı hello Test çıkışı bölmesinde görüntülenir. 

Merhaba üzerinde ı hello runbook düzenleme için açarak Hello Test denetimi bir runbook için açın ve **Test bölmesi** düğmesi.

![Test bölmesi düğmesi](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

herhangi bir giriş parametreleri ve hello runbook üzerinde hello tıklatarak başlatabilirsiniz Hello Test denetimi ister **Başlat** düğmesi.

![Test denetimi düğmeleri](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>Grafik runbook yayımlama
Azure Otomasyonu içindeki her runbook'un bir taslak ve bir yayımlanmış sürümü vardır. Yalnızca hello yayımlanan sürüm kullanılabilir toobe çalıştırmak ve yalnızca hello taslak sürüm düzenlenebilir. Merhaba yayımlanan sürüm herhangi bir değişiklik toohello Taslak sürümü tarafından etkilenmez. Merhaba Taslak sürümü hazır toobe kullanılabilir olduğunda, hangi hello yayımlanan sürüm hello taslak sürümle değiştirebilirsiniz yayımlayın.

Bir grafik runbook düzenleme ve üzerinde hello tıklatarak hello runbook açarak yayımlayabilirsiniz **Yayımla** düğmesi.

![Yayımla düğmesi](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

Bir runbook henüz yayımlanmadı zaman durumuna sahip **yeni**.  Yayımlandığında, durumuna sahip **yayımlanan**.  Merhaba runbook yayımlandıktan sonra hello taslak ve yayımlanan sürümleri farklı düzenlerseniz, hello runbook durumuna sahip **düzenleme**.

![Runbook durumları](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

Ayrıca bir runbook'un hello seçeneği toorevert toohello yayımlanan sürümü vardır.  Bu hemen hello runbook son yayımlandığı ve hello runbook'un taslak sürümünü hello hello yayımlanan sürümüyle değiştirir sonra yapılan tüm değişiklikleri atar.

![Toopublished düğmesi geri](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>Etkinlikler
Bir runbook'un hello yapı taşları etkinliklerdir.  Bir etkinlik PowerShell cmdlet, bir alt runbook veya iş akışı etkinlik olabilir.  Bir etkinlik toohello runbook sağ hello kitaplığı denetimi tıklatarak ve seçerek eklemek **toocanvas eklemek**.  Ardından, tıklatın ve hello üzerinde herhangi bir yere tuvale istediğiniz gibi hello etkinlik tooplace sürükleyin.  Merhaba hello tuval üzerinde hello Etkinliğin başlangıç konumunu hello işlemi hello runbook'un herhangi bir şekilde etkilemez.  En uygun toovisualize bulur ancak runbook'unuz düzeni için kendi işlemi. 

![Toocanvas Ekle](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

Merhaba tuvale tooconfigure Hello faaliyete hello yapılandırma dikey penceresinde özelliklerini ve parametreleri seçin.  Merhaba değiştirebileceğiniz **etiket** açıklayıcı tooyou olan hello etkinlik toosomething biri.  Merhaba özgün cmdlet'i hala çalıştırıldığı, basitçe hello grafik Düzenleyicisi'nde kullanılacak görünen adını değiştirmek.  Merhaba etiket hello runbook içinde benzersiz olmalıdır. 

### <a name="parameter-sets"></a>Parametre kümeleri
Bir parametre kümesi belirli bir cmdlet için değerleri kabul hello zorunlu ve isteğe bağlı parametreleri tanımlar.  Tüm cmdlet'ler, en az bir parametre kümesi ve bazı birden çok sahiptir.  Bir cmdlet birden fazla parametre kümesine varsa, parametreleri yapılandırmadan önce kullanacağınız hangisinin seçmelisiniz.  yapılandırabileceğiniz hello parametreleri seçtiğiniz hello parametre kümesi üzerinde bağlıdır.  Merhaba parametre kümesi seçerek bir etkinlik tarafından kullanılan değiştirebileceğiniz **parametre** ve başka bir kümesini seçme.  Bu durumda, yapılandırdığınız tüm parametre değerlerini kaybolur.

Aşağıdaki örneğine hello üç parametre kümeleri hello Get-AzureRmVM cmdlet'i vardır.  Merhaba parametre kümeleri birini seçene kadar parametre değerlerini yapılandıramazsınız.  Merhaba ListVirtualMachineInResourceGroupParamSet parametre kümesi kaynak grubundaki tüm sanal makineleri döndürmek için ve isteğe bağlı bir parametre vardır.  Merhaba GetVirtualMachineInResourceGroupParamSet tooreturn istediğiniz ve iki zorunlu ve isteğe bağlı bir parametre olan hello sanal makine belirtmenizi sağlar.

![Parametre kümesi](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>Parametre değerleri
Bir parametre için değer belirttiğinizde, hello değeri belirtilen nasıl bir veri kaynağı toodetermine seçin.  Bu parametre için geçerli değerler hello için belirli bir parametre kullanılabilir hello veri kaynakları bağlıdır.  Örneğin, Null, null değerlere izin vermiyor bir parametre için kullanılabilir bir seçenek olmaz.

| Veri kaynağı | Açıklama |
|:--- |:--- |
| Sabit değer |Merhaba parametresi için bir değer yazın.  Bu, yalnızca şu veri türlerini hello için kullanılabilir: Int32, Int64, dize, Boolean, DateTime, anahtarı. |
| Etkinlik çıkışı |Merhaba geçerli etkinliği hello iş akışında önündeki bir etkinliğin çıkışı.  Tüm geçerli etkinlikleri listelenir.  Yalnızca hello etkinlik toouse çıktısını hello parametre değeri seçin.  Birden fazla özelliğe sahip bir nesne Hello etkinlik çıkışı yapıyorsa hello etkinlik seçtikten sonra hello özelliğinin hello adını yazabilirsiniz. |
| Runbook giriş |Runbook giriş parametresi giriş toohello etkinlik parametresini seçin. |
| Değişken varlığı |Bir Otomasyon değişkeni giriş olarak seçin. |
| Kimlik bilgisi varlığı |Otomasyon kimlik bilgileri giriş olarak seçin. |
| Sertifika varlığı |Bir Otomasyon sertifikası giriş olarak seçin. |
| Bağlantı varlığı |Otomasyon bağlantısı giriş olarak seçin. |
| PowerShell ifadesi |Basit belirtin [PowerShell ifadesi](#powershell-expressions).  Merhaba ifade hello parametre değeri için kullanılan hello etkinliği ve hello sonucu önce değerlendirilir.  Bir etkinlik veya runbook giriş parametresi değişkenleri toorefer toohello çıkışını kullanabilirsiniz. |
| Yapılandırılmamış |Önceden yapılandırılmış herhangi bir değer temizler. |

#### <a name="optional-additional-parameters"></a>İsteğe bağlı ek parametreler
Tüm cmdlet'ler hello seçeneği tooprovide ek parametreler sahip olur.  Bunlar, PowerShell genel parametreleri veya diğer özel parametreler olan.  PowerShell sözdizimini kullanarak parametreler burada sağlayabilir içeren bir metin kutusu sunulur.  Örneğin, toouse hello **ayrıntılı** ortak parametresi belirtirsiniz **"-Verbose: $True"**.

### <a name="retry-activity"></a>Etkinlik yeniden deneyin
**Yeniden deneme davranışını** belirli bir koşul yerine getirilene kadar birden çok kez çalıştırmak bir etkinlik toobe sağlayan çok benzer bir döngü şekilde.  Birden çok kez çalıştırmanız, hata potansiyeli etkinlikler için bu özelliği kullanabilirsiniz ve birden fazla başarı için denemek veya geçerli veriler için hello etkinliğin hello çıkış bilgileri test.    

Bir etkinlik için retry etkinleştirdiğinizde, gecikme ve bir koşul ayarlayabilirsiniz.  Merhaba gecikme, (saniyeler veya dakikalar içinde ölçülür) hello süre hello etkinlik yeniden çalıştırmadan önce bu hello runbook bekler.  Ardından gecikme belirtilirse, hemen tamamlandıktan sonra hello etkinlik yeniden çalışır. 

![Etkinlik yeniden deneme gecikmesi](media/automation-graphical-authoring-intro/retry-delay.png)

Merhaba yeniden deneme koşulu her zaman hello etkinliğin çalıştıktan sonra değerlendirilen bir PowerShell ifadesidir.  Merhaba ifade tooTrue çözümlenirse, hello etkinlik yeniden çalıştırır.  Merhaba ifade tooFalse çözümlenirse sonra hello etkinlik yeniden çalıştırmaz ve hello runbook toohello sonraki etkinliği taşır. 

![Etkinlik yeniden deneme gecikmesi](media/automation-graphical-authoring-intro/retry-condition.png)

Merhaba yeniden deneme koşulu erişim tooinformation hello etkinlik yeniden deneme hakkında sağlar $RetryData adında bir değişkeni kullanabilirsiniz.  Bu değişken, aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| NumberOfAttempts |Etkinlik hello sayısı yapılmadı. |
| Çıktı |Merhaba çıktısını son hello etkinliğini çalıştırın. |
| TotalDuration |Zaman aşımına hello etkinlik başlatıldığından bu yana geçen hello ilk kez. |
| StartedAt |UTC biçiminde hello etkinlik süre önce başlatıldı. |

Aşağıda verilmiştir etkinlik örnekleri koşulları yeniden deneyin.

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

Bir etkinlik için bir yeniden deneme koşulu yapılandırdıktan sonra iki görsel ipuçları tooremind hello etkinlik içerir.  Hello etkinliğinde sunulur ve hello etkinlik hello yapılandırmasını gözden geçirirken hello diğer olur.

![Etkinlik yeniden deneme görsel göstergeleri](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>İş akışı komut dosyası denetimi
Kod PowerShell veya PowerShell iş akışı komut dosyası, aksi takdirde kullanılamayabilir sipariş tooprovide işlevindeki yazılmış grafik runbook hello türüne bağlı olarak kabul özel bir aktivite denetimdir.  Parametreleri kabul edemez, ancak etkinlik çıkışı ve runbook giriş parametreleri için değişkenleri kullanabilirsiniz.  Bu durumda, giden bağlantı olmadıkça toohello veri yoluna hello runbook toohello çıktısını eklenir hello etkinlik herhangi bir çıktı eklenir.

Örneğin hello aşağıdaki kodu tarih hesaplamaları $NumberOfDays adlı bir runbook giriş değişken kullanarak gerçekleştirir.  Merhaba runbook'taki izleyen etkinlikler tarafından kullanılan çıkış toobe olarak hesaplanan tarih saat sonra gönderir.

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>Bağlantılar ve iş akışı
A **bağlantı** grafik bir runbook'ta iki etkinlik bağlanır.  Merhaba kaynak etkinliği toohello hedef etkinliğinden ok olarak hello tuval üzerinde görüntülenir.  Merhaba etkinlikleri hello ok hello yönde hello hedef etkinlik hello kaynak etkinliği tamamlandıktan sonra Başlangıç çalıştırın.  

### <a name="create-a-link"></a>Bağlantı oluşturma
Hello şekli hello altındaki seçme hello kaynak etkinliği tarafından iki etkinlik ve tıklatmak hello daire arasında bir bağlantı oluşturun.  Merhaba ok toohello hedef etkinlik ve yayın sürükleyin.

![Bağlantı oluşturma](media/automation-graphical-authoring-intro/create-link-revised20165.png)

Merhaba bağlantı tooconfigure hello yapılandırma dikey penceresinde özelliklerini seçin.  Bu, aşağıdaki tablonun hello açıklanan hello bağlantı türü dahil edilir.

| Bağlantı türü | Açıklama |
|:--- |:--- |
| İşlem hattı |Merhaba hedef etkinlik, hello kaynak etkinliğinden her nesne çıktısı için bir kez çalıştırılır.  Merhaba kaynak etkinliği hiçbir çıkış sonuçlanırsa hello hedef etkinlik çalışmaz.  Çıktı hello kaynak etkinliğinden bir nesne olarak kullanılabilir. |
| Sırası |Merhaba hedef etkinlik yalnızca bir kez çalışır.  Bu nesneleri içeren bir dizi hello kaynak etkinliğinden alır.  Çıktı hello kaynak etkinliğinden nesnelerinin bir dizisi kullanılabilir. |

### <a name="starting-activity"></a>Başlangıç etkinliği
Bir grafik runbook gelen bağlantısına sahip olmayan tüm etkinlikleri ile başlar.  Bu, genellikle hello runbook etkinlik başlangıç hello olarak davranan yalnızca bir etkinlik olacaktır.  Birden çok etkinliği bir gelen bağlantı yoksa, hello runbook paralel olarak çalıştırarak başlar.  Her tamamlar, ardından hello bağlantılar toorun diğer etkinlikleri takip edecektir.

### <a name="conditions"></a>Koşullar
Bir bağlantı bir koşul belirttiğinizde, hello koşulu tootrue çözümlenirse hello hedef etkinlik yalnızca çalıştırılır.  Genellikle, bir koşul tooretrieve hello çıktı hello kaynak etkinliğinden $ActivityOutput değişkeni de kullanır.  

Ardışık Düzen bağlantısına için tek bir nesne için bir koşul belirtin ve hello koşul için her nesne çıktı hello kaynak etkinliği tarafından değerlendirilir.  Merhaba hedef etkinlik ardından hello koşulu karşılayan her bir nesne için çalıştırın.  Adlı kaynak grubu içindeki sanal makineler hello yalnızca örneğin, Get-AzureRmVm bir kaynak etkinlikle sözdizimi aşağıdaki hello koşullu ardışık düzen bağlantı tooretrieve için kullanılabilecek *Group1*.  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

Tüm nesneleri çıktı hello kaynak etkinliğinden içeren tek bir dizi döndürdü beri dizisi bağlantı için hello koşulu yalnızca bir kez değerlendirilir.  Bu nedenle, bir dizi bağlantı gibi bir ardışık düzen bağlantısına filtreleme için kullanılamaz ancak yalnızca hello sonraki etkinliği çalıştırmak olup olmadığını belirler. Örneğin VM Başlat runbook etkinlikleri kümesi aşağıdaki hello alın.<br> ![Dizileri ile koşullu bağlantı](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
Doğrulama değerleri tootwo runbook giriş parametreleri VM adını ve hello uygun eylemi tootake olan sipariş toodetermine kaynak grubu adını temsil eden sağlanan - tek bir VM'ye Başlat üç farklı sıra bağlantıları vardır, hello tüm sanal makineleri Başlat kaynak grubu veya bir Abonelikteki tüm VM'ler.  Connect tooAzure ve Get tek VM arasında Hello dizisi bağlantı için hello koşul mantığı şöyledir:

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

Bir koşullu bağlantı kullandığınızda, kullanılabilir hello kaynak etkinliği tooother etkinliklerden o şubedeki hello veri hello koşul tarafından filtrelenir.  Bir etkinlik hello kaynak toomultiple bağlantılar ise, her dalda kullanılabilir tooactivities toothat şube bağlanma hello bağlantı hello koşulunda bağlıdır veri hello.

Örneğin, hello **Start-AzureRmVm** aşağıdaki hello runbook'taki etkinlik tüm sanal makineleri başlatır.  İki koşullu bağlantıları vardır.  Merhaba ilk koşullu bağlantı kullanan hello ifade *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - eq $true* hello Start-AzureRmVm etkinliği başarıyla tamamlanırsa toofilter.  Merhaba kullanır ikinci hello ifade *$ActivityOutput ['Start-AzureRmVM']. IsSuccessStatusCode - ne $true* hello Start-AzureRmVm etkinlik toostart hello sanal makine başarısız olursa toofilter.  

![Koşullu bağlantı örneği](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

Merhaba ilk bağlantı izler ve Get-AzureVM hello etkinlik çıkışı kullanan herhangi bir etkinliği yalnızca Get-AzureVM çalıştırıldığı hello zamanında başlatılan hello sanal makineleri alır.  Merhaba ikinci bağlantıya izleyen herhangi bir etkinliği yalnızca Get-AzureVM çalıştırıldığı hello aynı anda durdurulan hello hello sanal makineleri alır.  Merhaba üçüncü bağlantı aşağıdaki herhangi bir etkinlik çalışan durumlarına bakılmaksızın tüm sanal makineler alırsınız.

### <a name="junctions"></a>Kavşakları
Bir birleşim tüm gelen dalları tamamlanana kadar bekler özel bir etkinliktir.  Toorun bu sayede birden fazla etkinlikleri paralel ve tüm geçmeden önce tamamladığınızdan emin olun.

Bir birleşim gelen bağlantıları sınırsız sayıda varken bu bağlantıları geçmeyen biri bir işlem hattı olabilir.  Gelen sırası bağlantıları Hello sayısı sınırlı değildir.  Birden çok gelen ardışık düzen bağlantılarla toocreate hello birleşim izin verecek ve hello runbook'u kaydedin, ancak çalışırken başarısız olur.

Aşağıdaki örnek Hello sanal makineler kümesi toothose makineler uygulanan düzeltme ekleri toobe eşzamanlı olarak indirme sırasında başlayan bir runbook bir parçasıdır.  Bir birleşim kullanılan tooensure olan hello runbook devam etmeden önce her iki işlem tamamlandı.

![Birleşim](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>Döngüler
Bir döngü sonunda bağlantılar tooits kaynak yedeklemeniz etkinlik veya tooanother etkinlik tooits kaynak bir hedef etkinlik geri bağlantılar durumdur.  Döngüleri grafik yazma şu anda izin verilmiyor.  Runbook'unuz bir döngü sahipse, düzgün şekilde kaydedecek ancak çalışırken bir hata iletisi alırsınız.

![Döngüsü](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>Etkinlikler arasında veri paylaşımı
Çıkış giden bir bağlantı içeren bir etkinlik tarafından herhangi bir veri toohello yazılır *veri yoluna* hello runbook için.  Merhaba runbook'taki her etkinlik hello veri yoluna toopopulate parametre değerlerine verileri kullanma veya komut dosyası kodu içerir.  Bir etkinlik hello çıktı hello iş akışındaki herhangi bir önceki etkinliği erişebilir.     

Hello veriler toohello veri yoluna nasıl yazılır hello etkinlik bağlantıdaki hello türüne bağlıdır.  İçin bir **ardışık düzen**, hello verilerdir çıkış katları nesneler olarak.  İçin bir **dizisi** bağlantı, hello çıkış dizisi olarak verilerdir.  Tek bir değer varsa, tek bir öğe dizisi olarak çıkış olacaktır.

İki yöntemden birini kullanarak hello veri yoluna verilere erişebilir.  İlk kullanarak bir **etkinlik çıkışı** veri kaynağı toopopulate başka bir etkinliğin bir parametre.  Merhaba çıktı bir nesne ise, tek bir özellik belirtebilirsiniz.

![Etkinlik çıkışı](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

Bir etkinlik hello çıktısını de alabilirsiniz bir **PowerShell ifadesi** veri kaynağı veya bir **iş akışı betiği** ActivityOutput değişkeniyle etkinlik.  Merhaba çıktı bir nesne ise, tek bir özellik belirtebilirsiniz.  ActivityOutput değişkenleri sözdizimi aşağıdaki hello kullanın.

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>Kontrol noktaları
Ayarlayabileceğiniz [kontrol noktaları](automation-powershell-workflow.md#checkpoints) seçerek bir grafik PowerShell iş akışı runbook'ta *denetim noktası runbook* herhangi bir etkinlik üzerinde.  Bu hello etkinlik çalıştıktan sonra ayarlanmış bir denetim noktası toobe neden olur.

![Denetim noktası](media/automation-graphical-authoring-intro/set-checkpoint.png)

Kontrol noktaları grafik PowerShell iş akışı runbook'ları yalnızca etkinleştirilen, grafik runbook'larında kullanılabilir değildir.  Merhaba runbook Azure cmdlet'lerini kullanıyorsa, hello runbook askıya alınır ve yeniden durumda Add-AzureRMAccount belirttiğinizde herhangi bir etkinliği izlemelisiniz farklı bir çalışan üzerinde bu kontrol noktasından. 

## <a name="authenticating-tooazure-resources"></a>Kimlik doğrulama tooAzure kaynakları
Azure kaynaklarını yöneten Azure automation'daki Runbook'lar kimlik doğrulaması tooAzure gerektirir.  Merhaba [farklı çalıştır hesabı](automation-offering-get-started.md#creating-an-automation-account) (aynı zamanda, başvurulan tooas bir hizmet sorumlusu) olan hello varsayılan yöntemi tooaccess Automation runbook'larıyla aboneliğinizdeki Azure Resource Manager kaynakları.  Merhaba ekleyerek bu işlevselliği tooa grafik runbook ekleyebilirsiniz **AzureRunAsConnection** hello PowerShell kullanarak bağlantı varlığı [Get-AutomationConnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) cmdlet'ini ve [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello tuvale. Bu örnekte aşağıdaki hello gösterilmiştir.<br>![Kimlik doğrulama etkinlikler olarak çalıştırmak](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
Merhaba farklı çalıştır bağlantısını Al etkinliği (yani Get-AutomationConnection) AzureRunAsConnection adlı bir sabit değer veri kaynağı ile yapılandırılır.<br>![Bağlantı yapılandırma olarak çalıştır](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
Merhaba sonraki etkinliği, Add-AzureRmAccount, kimliği doğrulanmış hello farklı çalıştır hesabı kullanmak için hello runbook'ta ekler.<br>
![Add-AzureRmAccount parametre kümesi](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Merhaba parametreler için **APPLİCATİONID**, **CERTIFICATETHUMBPRINT**, ve **TENANTID** toospecify hello hello özelliğinin adını çünkü hello alan yolu için gerekir Merhaba etkinlik birden fazla özelliğe sahip bir nesne çıkarır.  Aksi takdirde hello runbook yürüttüğünüzde çalışırken tooauthenticate başarısız olur.  Bu, runbook'unuzu hello ile farklı çalıştır hesabı en az bir tooauthenticate adresindeki ihtiyacınız olur.

toomaintain geriye doğru uyumluluk için bir Otomasyon oluşturan aboneleri hesabı kullanarak bir [Azure AD kullanıcı hesabı](automation-create-aduser-account.md) toomanage Azure Klasik dağıtım veya Azure Resource Manager kaynakları için yöntem tooauthenticate hello Merhaba Add-AzureAccount cmdlet'i ile bir [kimlik bilgisi varlığı](automation-credentials.md) erişim toohello Azure hesabı olan bir Active Directory kullanıcı temsil eden.

Add-AzureAccount etkinlik tarafından izlenen bir kimlik bilgisi varlığı toohello tuvali ekleyerek bu işlevselliği tooa grafik runbook ekleyebilirsiniz.  Add-AzureAccount hello kimlik bilgisi etkinlik kendi giriş için kullanır.  Bu örnekte aşağıdaki hello gösterilmiştir.

![Kimlik doğrulama etkinlikleri](media/automation-graphical-authoring-intro/authentication-activities.png)

Merhaba başlangıç hello runbook'un sonra her bir denetim noktası tooauthenticate sahip.  Bu, herhangi bir Checkpoint-Workflow etkinliği sonra ek Add-AzureAccount etkinlik ekleme anlamına gelir. Bir ek kimlik bilgisi gerekmez kullanabileceğiniz beri etkinlik hello aynı 

![Etkinlik çıkışı](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Giriş ve çıkış Runbook
### <a name="runbook-input"></a>Runbook giriş
Merhaba geçerli bir alt öğesi olarak kullanılıyorsa, hello hello Azure portalı üzerinden veya başka bir runbook'tan runbook başlattığınızda bir runbook ya da bir kullanıcıdan giriş gerektirebilir.
Örneğin, bir sanal makine oluşturur bir runbook'unuz varsa hello runbook her başlattığınızda hello sanal makinenin hello adı gibi tooprovide bilgileri ve diğer özellikleri gerekebilir.  

Bir tanımlayarak bir runbook için giriş kabul edin veya daha fazla giriş parametreleri.  Her zaman hello runbook başlatıldığında bu parametreler için değerler sağlayın.  Hello Azure portal ile bir runbook'u başlattığınızda bu hello her hello runbook'un giriş parametreleri için değerleri tooprovide ister.

Bir runbook'un giriş parametreleri hello tıklatarak erişebilirsiniz **giriş ve çıkış** hello runbook araç çubuğunda.  

![Runbook giriş çıkış](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

Merhaba açılır **giriş ve çıkış** , var olan bir giriş parametresi düzenleyin veya tıklatarak yeni bir tane oluşturun denetim **giriş Ekle**. 

![Giriş Ekle](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

Her giriş parametresi, aşağıdaki tablonun hello hello özelliklerinde tarafından tanımlanır.

| Özellik | Açıklama |
|:--- |:--- |
| Ad |Merhaba hello parametrenin benzersiz adı.  Bu, yalnızca alfa sayısal karakterler içerebilir ve bir boşluk içeremez. |
| Açıklama |Merhaba giriş parametresi için isteğe bağlı bir açıklama. |
| Tür |Merhaba parametre değeri için beklenen veri türü.  Hello Azure portal hello veri türü için uygun bir denetim için giriş isterken her parametre için sağlayacaktır. |
| Zorunlu |Bir değer hello parametresi için sağlanan olup olmadığını belirtir.  tanımlanmış bir varsayılan değeri yok zorunlu her parametre için bir değer belirtmezseniz, hello runbook başlatılamıyor. |
| Varsayılan değer |Bir sağlanmazsa, hello parametresi için hangi değerin kullanıldığını belirtir.  Bu Null ya da belirli bir değer olabilir. |

### <a name="runbook-output"></a>Runbook çıkışı
Giden bir bağlantı yok herhangi bir etkinlik tarafından oluşturulan veriler toohello eklenecek [hello runbook çıktısını](http://msdn.microsoft.com/library/azure/dn879148.aspx).  Merhaba çıktı hello runbook işi ile kaydedilir ve hello runbook bir alt öğesi olarak kullanılabilir tooa üst runbook kullanılmasıdır.  

## <a name="powershell-expressions"></a>PowerShell ifadeleri
Grafik yazma hello avantajlarından biri, hello özelliği toobuild PowerShell ilişkin minimum bilgi ile bir runbook ile sağlamaktadır.  Şu anda, ancak belirli doldurmak için tooknow biraz PowerShell gereksiniminiz [parametre değerlerini](#activities) ve ayarı için [bağlantı koşulları](#links-and-workflow).  Bu bölümde tooPowerShell ifadeler ile tanıdık olmayabilir olan kullanıcılar için bir giriş sağlar.  PowerShell tam ayrıntıları şurada bulunabilir [ile Windows PowerShell komut dosyası](http://technet.microsoft.com/library/bb978526.aspx). 

### <a name="powershell-expression-data-source"></a>PowerShell ifadesi veri kaynağı
Bir PowerShell ifadesi bir veri kaynağı toopopulate hello değeri olarak kullanabileceğiniz bir [Etkinlik parametresi](#activities) bazı PowerShell kod hello sonuçlarla.  Bu tek satırlık bir bazı basit işlevi veya karmaşık bir mantık gerçekleştirmek birden çok satır gerçekleştirir kod olabilir.  Herhangi bir çıktı olmayan komutundan tooa atanan değişkenidir çıktı toohello parametre değeri. 

Örneğin, komutu aşağıdaki hello hello geçerli tarih çıktı. 

    Get-Date

Merhaba aşağıdaki komutları hello dizeden oluşturma geçerli tarihi ve tooa değişkeni atayın.  Merhaba değişkeni Merhaba içeriğine sonra toohello çıkış gönderilir 

    $string = "hello current date is " + (Get-Date)
    $string

Merhaba aşağıdaki komutları hello geçerli tarih değerlendirin ve hello geçerli günde bir hafta sonu veya haftanın günü olup olmadığını belirten bir dize döndürür. 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>Etkinlik çıkışı
önceki bir etkinliğin hello runbook'taki sözdizimi aşağıdaki hello kullan hello $ActivityOutput değişkenle toouse hello çıkışı.

    $ActivityOutput['Activity Label'].PropertyName

Örneğin, bir sanal makinenin adını hello gerektiren bir özellik olmayan bir etkinliği olabilir; bu durumda ifade aşağıdaki hello kullanabilirsiniz.

    $ActivityOutput['Get-AzureVm'].Name

Yalnızca bir özellik olduktan sonra yerine yeni bir sanal makine nesne hello gereken hello özelliği döndürür, nesnenin tamamı hello kullanarak hello sözdizimi aşağıdaki.

    $ActivityOutput['Get-AzureVm']

Metin toohello sanal makine adı art arda ekler hello aşağıdaki gibi daha karmaşık bir ifadede bir etkinlik hello çıktısını de kullanabilirsiniz.

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>Koşullar
Kullanım [Karşılaştırma işleçleri](https://technet.microsoft.com/library/hh847759.aspx) toocompare değerleri veya bir değeri belirtilen desenle eşleşip eşleşmediğini belirler.  Bir karşılaştırma $true veya $false değerini döndürür.

Örneğin, aşağıdaki koşul hello hello sanal makine bir etkinliğin adlı olup olmadığını belirler *Get-AzureVM* şu anda *durduruldu*. 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

Merhaba şu koşul denetimleri hello aynı sanal makine herhangi başka bir durumda olup olmadığını *durduruldu*.

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

Birden çok koşul kullanarak katılabilirsiniz bir [mantıksal işleç](https://technet.microsoft.com/library/hh847789.aspx) gibi **- ve** veya **- veya**.  Örneğin, Hello hello önceki örnekte aynı sanal makineye bir durumda olup hello şu denetimleri koşul *durduruldu* veya *durdurma*.

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>Hashtable'da
[Hashtable'da](http://technet.microsoft.com/library/hh847780.aspx) değer kümesini döndürmek için yararlı olan ad/değer çiftleri.  Özellikler belirli etkinlikler için basit bir değer yerine bir hashtable bekleyebilir.  Hashtable tooas bir sözlük başvurulan olarak da görebilirsiniz. 

Bir karma tablosu söz dizimi aşağıdaki hello ile oluşturun.  Bir karma tablosu girdileri herhangi bir sayıda içerebilir ancak her bir ad ve değer tarafından tanımlanır.

    @{ <name> = <value>; [<name> = <value> ] ...}

Örneğin, hello ifadesini hello veri kaynağında bir internet arama değerlerini içeren bir hashtable beklenen bir etkinlik parametresi için kullanılan bir hashtable toobe oluşturur.

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

Merhaba aşağıdaki örnek kullanır adlı bir etkinliğin çıkışı *Twitter bağlantısını Al* toopopulate bir karma tablosu.

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>Sonraki Adımlar
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md) 
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)
* runbook türleri, avantajları ve sınırlamaları, hakkında daha fazla tooknow bakın [Azure Automation runbook türleri](automation-runbook-types.md)
* toounderstand tooauthenticate kullanarak hello nasıl Automation farklı çalıştır hesabı için bkz: [yapılandırma Azure farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md)

