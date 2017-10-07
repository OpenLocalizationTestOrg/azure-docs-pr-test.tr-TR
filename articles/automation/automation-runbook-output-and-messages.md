---
title: "aaaRunbook çıkışı ve iletileri Azure Automation | Microsoft Docs"
description: "Nasıl toocreate ve alma çıkış ve hata iletilerini Azure automation'daki runbook'lar Desribes."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Runbook çıkışı ve iletileri Azure Automation
Çoğu Azure Automation runbook bir hata iletisi toohello kullanıcı gibi bir çıkış çeşit erişebilir veya karmaşık bir nesne başka bir iş akışı tarafından tüketilen toobe amaçlar. Windows PowerShell sağlar [birden çok akış](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) toosend çıktısını bir komut dosyası veya iş akışı. Azure Otomasyonu çalışır her bu akışları farklı ve nasıl için en iyi uygulamaları izlemelisiniz toouse her bir runbook oluştururken.

Merhaba aşağıdaki tabloda her hello akışlar ve hello Azure Yönetim Portalı'ndaki davranışları kısa bir açıklamasını hem yayımlanan bir runbook çalıştırılırken hem de sağlar [bir runbook'u test](automation-testing-runbook.md). Her akış hakkında ek ayrıntılar sonraki bölümlerde verilmiştir.

| Akış | Açıklama | Yayımlanma | Test etme |
|:--- |:--- |:--- |:--- |
| Çıktı |Nesneleri diğer runbook'lar tarafından tüketilen toobe amaçlanmıştır. |Toohello iş geçmişine yazılır. |Merhaba Test çıkışı bölmesinde görüntülenir. |
| Uyarı |Merhaba kullanıcıya yönelik uyarı iletisi. |Toohello iş geçmişine yazılır. |Merhaba Test çıkışı bölmesinde görüntülenir. |
| Hata |Merhaba kullanıcıya yönelik hata iletisi. Bir özel durumun aksine hello runbook varsayılan olarak bir hata iletisinden sonra devam eder. |Toohello iş geçmişine yazılır. |Merhaba Test çıkışı bölmesinde görüntülenir. |
| Ayrıntılı |Genel ya da hata ayıklama bilgileri sağlayan iletiler. |Ayrıntılı günlük kaydını hello runbook için açık olup olmadığını yalnızca toojob geçmişine yazılır. |Yalnızca $VerbosePreference tooContinue hello runbook'ta ayarlandıysa hello Test çıkışı Bölmesi'nde görüntülenir. |
| İlerleme durumu |Önce ve hello runbook'taki her etkinlikten sonra otomatik olarak oluşturulan kayıtlar. etkileşimli bir kullanıcı için amaçlandığından hello runbook kendi ilerleme durumu kayıtlarını toocreate çalışmamalıdır. |İlerleme durumu günlük kaydı hello runbook için açık olup olmadığını yalnızca toojob geçmişine yazılır. |Test çıkış Bölmesi'Hello görüntülenmez. |
| Hata ayıklama |Etkileşimli bir kullanıcıya yönelik iletiler. Runbook'larda kullanılmamalıdır. |Toojob geçmişine yazılmaz. |TooTest çıkış bölmesi yazılmaz. |

## <a name="output-stream"></a>Çıkış akışı
Merhaba çıkış akışı, doğru çalıştığı zaman bir komut dosyası veya iş akışı tarafından oluşturulan nesnelerin çıkışı için tasarlanmıştır. Azure Otomasyonu'nda Bu akış öncelikle tarafından tüketilen amaçlanan nesneler toobe için kullanılan [üst hello geçerli runbook'u çağıran runbook'ları](automation-child-runbooks.md). Olduğunda, [bir runbook'u satır içi olarak çağırdığınızda](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution) üst runbook'tan veri hello çıkış akışı toohello üst öğeden döndürür. Merhaba runbook başka bir runbook tarafından hiçbir zaman çağrılacağı biliyorsanız hello çıkış akışı toocommunicate genel bilgiler geri toohello kullanıcı yalnızca kullanmanız gerekir. En iyi uygulama, ancak genellikle hello kullanmanız [ayrıntılı akış](#Verbose) toocommunicate genel bilgiler toohello kullanıcı.

Veri toohello çıkış akışı kullanarak yazabilirsiniz [Write-Output](http://technet.microsoft.com/library/hh849921.aspx) veya hello nesne hello runbook'ta kendi satırına koyarak kullanılabilir.

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>Bir işlevden çıkış
Runbook'unuza dahil edilen bir işlevde toohello çıkış akışı yazdığınızda hello çıkış geri toohello runbook geçirilir. Ardından Hello runbook bu çıkışı tooa değişken atarsa, toohello çıkış akışına yazılmaz. Diğer akışlardan hello işlevi içinde tooany yazma toohello hello runbook için buna karşılık gelen akışa yazar.

Aşağıdaki örnek runbook hello göz önünde bulundurun.

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


Merhaba runbook işi için çıkış akışı Hello olacaktır:

    Output inside of function
    Output outside of function

Merhaba runbook işi için ayrıntılı akış Hello olacaktır:

    Verbose outside of function
    Verbose inside of function

Merhaba runbook yayımladıktan sonra ve, başlamadan önce ayrıca ayrıntılı sipariş tooget hello ayrıntılı akış çıkışı hello runbook ayarlarını günlüğe açmanız gerekir.

### <a name="declaring-output-data-type"></a>Bildiren çıktı veri türü
Bir iş akışı hello kullanarak çıktısını hello veri türünü belirtebilirsiniz [OutputType özniteliğini](http://technet.microsoft.com/library/hh847785.aspx). Bu özniteliğin çalışma zamanı sırasında herhangi bir etkisi olmaz ancak hello beklenen çıktı hello runbook'un tasarım zamanında bir göstergesi toohello runbook Yazar sağlar. Runbook'lar için Hello araç takımı tooevolve devam ettikçe, çıkış veri türlerinin tasarım zamanında bildirilmesinin önemi hello önemi artacaktır. Sonuç olarak, en iyi uygulamadır tooinclude oluşturduğunuz tüm runbook'lara bu bildirimi olur.

Çıktı türleri örnek listesi aşağıdadır:

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

Merhaba aşağıdaki örnek runbook bir dize nesnesi çıkışı yapar ve çıkış türü bildirimini içerir. Runbook'unuz belirli bir türde dizi çıkışı yapıyorsa, yine hello türü hello türü karşılıklı tooan dizisi olarak belirtmelisiniz.

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

bir çıkış türü Grapical veya grafik PowerShell iş akışı runbook'ları toodeclare hello seçebilirsiniz **giriş ve çıkış** menü seçeneğini ve hello hello adında türünü çıktı türü.  Merhaba tam .NET sınıf adı toomake kullanmanızı öneririz, üst runbook'tan başvururken kolayca tanımlanabilen.  Bu o sınıf toohello veri yolu hello runbook'taki tüm hello özelliklerini gösterir ve bunları günlüğe kaydetme ve hello runbook'taki diğer etkinlikler için değerler olarak başvuran koşullu mantık için kullanırken büyük bir esneklik sağlar.<br> ![Runbook giriş ve çıkış seçeneği](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

Aşağıdaki örnek hello, bu özellik iki grafik runbook'lar toodemonstrate sunuyoruz.  Biz hello modüler runbook tasarım modeli uygularsanız, hello hizmet veren bir runbook sahibiz *kimlik doğrulaması Runbook şablonu* hello farklı çalıştır hesabı Azure kullanarak kimlik doğrulaması yönetme.  Normalde hello çekirdek mantığını tooautomate belirli bir senaryo gerçekleştireceği, bizim ikinci runbook bu durumda tooexecute hello geçiyor *kimlik doğrulaması Runbook şablonu* ve hello sonuçları tooyour görüntülemek **Test** çıkış bölmesi.  Normal koşullar altında biz kaynak yararlanmayı hello çıkış karşı hello alt runbook'tan bir şeyler bu runbook gerekir.    

Merhaba hello temel mantığını işte **AuthenticateTo Azure** runbook.<br> ![Runbook şablonu örnek kimliğini](media/automation-runbook-output-and-messages/runbook-authentication-template.png).  

Merhaba çıktı türü içeren *Microsoft.Azure.Commands.Profile.Models.PSAzureContext*, hello kimlik doğrulama profili özellikleri döndürecektir.<br> ![Runbook'u çıktı türü örneği](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

Bu runbook çok düz İleri olmakla birlikte, bir yapılandırma öğesi toocall burada çıkışı yoktur.  Merhaba son etkinlik hello yürütme **Write-Output** cmdlet'i ve yazma işlemleri hello profil verileri tooa $_ değişkeni hello için bir PowerShell ifadesi kullanarak **Inputobject** için gerekli olan parametre cmdlet'ini kullanın.  

Merhaba ikinci runbook için bu örnekte, adlı *Test ChildOutputType*, yalnızca iki etkinlik sunuyoruz.<br> ![Örnek alt türü Runbook çıkış](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

Merhaba ilk etkinliği çağırır hello **AuthenticateTo Azure** runbook ve hello ikinci etkinlik hello çalıştıran **Write-Verbose** hello cmdlet'iyle **veri kaynağı** , **Etkinlik çıkışı** ve hello değerini **alan yolu** olan **Context.Subscription.SubscriptionName**, hello bağlam hello çıktısını belirtme  **AuthenticateTo Azure** runbook.<br> ![Write-Verbose cmdlet parametresi veri kaynağı](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

Merhaba sonuçta çıktı hello abonelik hello adıdır.<br> ![Test-ChildOutputType Runbook sonuçları](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

Merhaba çıktı türü denetimi hello davranışını hakkında bir not.  Merhaba giriş hello çıktı türü alanında değer ve çıktı özellikleri dikey yazdığınızda, hello denetimi tarafından tanınan, giriş toobe sırada, yazdıktan sonra hello denetimi dışında tooclick sahip.  

## <a name="message-streams"></a>İleti akışları
Merhaba çıkış akışından farklı olarak, ileti hedeflenen toocommunicate bilgi toohello kullanıcı akışlarıdır. Farklı bilgi türleri için birden çok ileti akışı vardır ve her Azure Automation tarafından farklı şekilde ele alınır.

### <a name="warning-and-error-streams"></a>Uyarı ve hata akışları
Merhaba uyarı ve hata akışlarının bir runbook'ta oluşan hedeflenen toolog sorunlardır. Bir runbook yürütülür ve bir runbook test edildiğinde hello Test çıkış Bölmesi'hello Azure Yönetim Portalı'nda yer alan bunlar toohello iş geçmişine yazılır. Varsayılan olarak, hello runbook bir uyarı veya hatadan sonra yürütülmeye devam eder. Bu hello runbook askıya bir uyarı veya hata ayarlayarak belirleyebilirsiniz bir [tercih değişkeni](#PreferenceVariables) hello runbook'taki selamlama iletisine oluşturmadan önce. Örneğin, bir özel durum gibi toocause runbook toosuspend bir hata ayarlayın **$ErrorActionPreference** tooStop.

Hello kullanarak bir uyarı veya hata iletisi oluşturma [Write-Warning](https://technet.microsoft.com/library/hh849931.aspx) veya [yazma hatası](http://technet.microsoft.com/library/hh849962.aspx) cmdlet'i. Etkinlikler de toothese akışları yazabilirsiniz.

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>Ayrıntılı akış
Merhaba ayrıntılı ileti akışı hello runbook işlemi hakkında genel bilgi içindir. Merhaba itibaren [hata ayıklama akışı](#Debug) kullanılabilir olmayan bir runbook'ta ayrıntılı iletiler için hata ayıklama bilgileri kullanılmalıdır. Varsayılan olarak, yayımlanan runbook'lardan ayrıntılı iletiler hello iş geçmişinde depolanmaz. toostore ayrıntılı iletiler hello yapılandırma sekmesinde hello Azure Yönetim Portalı'nda hello runbook'un yayımlanan runbook'lar tooLog ayrıntılı kayıtları yapılandırın. Çoğu durumda, performans nedenleriyle runbook için ayrıntılı kayıtları günlüğe kaydetme değil, hello varsayılan ayarını korumalısınız. Bu seçenek yalnızca tootroubleshoot kapatabilir veya bir runbook'ta hata ayıklamak.

Zaman [bir runbook'u test](automation-testing-runbook.md), hello runbook ayrıntılı kayıtları yapılandırılmış toolog olsa ayrıntılı iletiler görüntülenmez. toodisplay ayrıntılı iletiler sırasında [bir runbook'u test](automation-testing-runbook.md), hello $VerbosePreference değişkeni tooContinue ayarlamanız gerekir. Bu değişken ayarlandığında, ayrıntılı iletiler hello Test çıkış Bölmesi'hello Azure portal, görüntülenir.

Hello kullanarak ayrıntılı ileti oluşturma [Write-Verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet'i.

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>Hata ayıklama akışı
Merhaba hata ayıklama akışının etkileşimli kullanıcı kullanılmaya yöneliktir ve runbook'larda kullanılmamalıdır.

## <a name="progress-records"></a>İlerleme durumu kayıtları
Yapılandırırsanız, bir runbook toolog ilerleme (sekmesinde hello yapılandırma hello Azure Portalı'nda hello runbook'un) kaydeder ve sonra önce ve her etkinliğin çalıştıktan sonra toohello iş geçmişine bir kayıt yazılır. Çoğu durumda, bir runbook için ilerleme durumu kayıtlarını sipariş toomaximize performans günlüğü değil, hello varsayılan ayarını korumalısınız. Bu seçenek yalnızca tootroubleshoot kapatabilir veya bir runbook'ta hata ayıklamak. Merhaba runbook yapılandırılmış toolog ilerleme durumu kayıtlarını olsa bile bir runbook'u test ederken ilerleme durumu iletileri görüntülenmez.

Merhaba [Write-Progress](http://technet.microsoft.com/library/hh849902.aspx) cmdlet olmadığından bir runbook'ta geçerli bu etkileşimli bir kullanıcı ile kullanılmak üzere tasarlanmıştır.

## <a name="preference-variables"></a>Tercih değişkenleri
Windows PowerShell kullanan [tercih değişkenleri](http://technet.microsoft.com/library/hh847796.aspx) toodetermine nasıl toorespond gönderilen toodata toodifferent çıkış akışlarını. Bu değişkenler bir runbook toocontrol toodata farklı akışlara gönderilen nasıl yanıt vereceğini ayarlayabilirsiniz.

Merhaba aşağıdaki tabloda geçerli runbook'ları ve varsayılan değerleri kullanılabilir hello tercih değişkenleri listeler. Bu tablo yalnızca bir runbook'ta geçerli olan hello değerleri içerdiğini unutmayın. Windows PowerShell Azure Otomasyonu dışında kullanıldığında hello tercih değişkenleri için ek değerler geçerlidir.

| Değişken | Varsayılan değer | Geçerli Değerler |
|:--- |:--- |:--- |
| WarningPreference |Devam |Durdur<br>Devam<br>SilentlyContinue |
| ErrorActionPreference |Devam |Durdur<br>Devam<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Durdur<br>Devam<br>SilentlyContinue |

Aşağıdaki tablonun hello hello davranışı runbook'larda geçerli hello tercih değişkeni değerleri için listeler.

| Değer | Davranışı |
|:--- |:--- |
| Devam |Merhaba iletiyi günlüğe kaydeder ve hello runbook'u yürütmeye devam eder. |
| SilentlyContinue |Merhaba iletiyi günlüğe kaydetmeden Hello runbook'u yürütmeye devam eder. Bu hello ileti yoksayılıyor hello etkisi vardır. |
| Durdur |Merhaba iletiyi günlüğe kaydeder ve hello runbook'u askıya alır. |

## <a name="retrieving-runbook-output-and-messages"></a>Runbook çıkışlarını ve iletilerini alma
### <a name="azure-portal"></a>Azure portalına
Merhaba hello işler sekmesinden bir runbook'un Azure portalından bir runbook işi hello ayrıntılarını görüntüleyebilirsiniz. Merhaba hello iş özetini görüntüler hello giriş parametreleri ve hello [çıkış akışı](#Output) hello iş ve bunlar ortaya çıktıysa özel durumlar hakkında ek toogeneral bilgi. Merhaba geçmişi hello gelen iletileri içerecektir [çıkış akışı](#Output) ve [uyarı ve hata akışları](#WarningError) toplama toohello içinde [ayrıntılı akış](#Verbose) ve [ilerleme durumu Kayıtları](#Progress) hello runbook yapılandırılmış toolog ayrıntılı ve ilerleme durumu kayıtlarını ise.

### <a name="windows-powershell"></a>Windows PowerShell
Windows PowerShell'de çıkışı ve iletileri hello kullanarak bir runbook'tan alabilirsiniz [Get-AzureAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet'i. Bu cmdlet hello işin kimliği hello ve hangi akış tooreturn belirlediğiniz akış adlı bir parametreye sahip gerektirir. Merhaba işin tüm akışlarını herhangi tooreturn belirtebilirsiniz.

Aşağıdaki örneğine hello bir örnek runbook'i ve sonra onu bekler toocomplete başlatır. Tamamlandığında, çıkış akışı hello işten toplanır.

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>Grafik yazma
Grafik runbook'lar için ek günlük etkinlik düzeyi izleme hello formunda kullanılabilir.  İzleme iki düzeyi vardır: temel ve ayrıntılı.  Temel izleme hello runbook artı bilgileri her bir etkinlik bitiş zamanı, deneme sayısı ve hello Etkinliğin başlangıç zamanı gibi tooany etkinlik yeniden deneme ilgili ve başlangıç hello görebilirsiniz.  Ayrıntılı izleme, her etkinlik için temel izleme artı girdi ve çıktı veri alın.  Şu anda hello izleme kayıtları izlemeyi etkinleştirdiğinizde, ayrıntılı günlük etkinleştirmelisiniz hello ayrıntılı akış kullanarak yazıldığını unutmayın.  İzlemenin etkin ile grafik runbook'lar için gerek yoktur toolog ilerleme durumu kayıtlarını hello temel izleme görevi görür aynı amaca hello ve daha bilgilendirici olduğundan.

![Görünüm grafik yazma iş akışları](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

Ekran yukarıda hello gelen, ayrıntılı günlük kaydı ve grafik runbook'lar için izlemeyi etkinleştirdiğinizde, çok daha fazla bilgi iş akışları görüntülemek hello üretimde kullanılabilir olduğunu görebilirsiniz.  Bu ek bilgiler ile runbook üretim sorunlarını gidermeye yönelik temel olabilir ve bu nedenle, yalnızca bu genel bir uygulama değil de, bunun için etkinleştirmeniz gerekir.    
Merhaba izleme kayıtları, özellikle çok sayıda olabilir.  Grafik runbook ile izleme, basit veya ayrıntılı izleme yapılandırmış olmanıza bağlı olarak Etkinlik başına iki toofour kaydı elde edebilirsiniz.  Sorun giderme için bu bilgileri tootrack hello ilerleme bir runbook'un gerekli olmadıkça, izlemeyi devre dışı tookeep isteyebilirsiniz.

**tooenable etkinlik düzeyi izleme, hello aşağıdaki adımları gerçekleştirin.**

1. Hello Azure Portal'da, Automation hesabınızı açın.
2. Tıklatın hello üzerinde **Runbook'lar** döşeme tooopen hello listesini.
3. Merhaba Runbook dikey penceresinde, tooselect runbook'lar listesinden bir grafik runbook'ı tıklatın.
4. Hello ayarları dikey penceresinde seçili hello runbook, tıklatın **günlüğe kaydetme ve izleme**.
5. Günlüğe kaydetme ve ayrıntılı kayıtları günlüğe altında dikey izleme üzerinde Hello tıklatın **üzerinde** tooenable ayrıntılı günlük kaydı ve udner etkinlik düzeyinde izlemeyi değiştirin hello izleme düzeyi çok**temel** veya **ayrıntılı**  ihtiyaç duyduğunuz izleme hello düzeyine bağlı.<br>
   
   ![Grafik yazma günlüğe kaydetme ve dikey izleme](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Microsoft Operations Management Suite (OMS) günlük analizi
Otomasyon runbook iş durumu ve iş akışları tooyour Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı gönderebilirsiniz.  Günlük analizi ile şunları yapabilirsiniz,

* Otomasyon işleriniz hakkında bilgi edinme 
* Bir e-posta veya uyarı (örneğin başarısız oldu veya askıya alınmış), runbook işi durumlarına dayalı tetikleyici 
* Gelişmiş sorgular, iş akışları yazma 
* İşlerini Automation hesaplarında ilişkilendirmek 
* İş Geçmişi zaman içinde görselleştirin    

Günlük analizi toocollect ile tooconfigure tümleştirme ilişkilendirmek ve hareket iş verilerine nasıl daha fazla bilgi için bkz: [Otomasyon tooLog analizi (OMS) iş durumu ve iş akışları iletmek](automation-manage-send-joblogs-log-analytics.md).

## <a name="next-steps"></a>Sonraki adımlar
* toolearn hakkında daha fazla runbook yürütme toomonitor runbook işleri ve diğer teknik ayrıntıları görmek nasıl [bir runbook işi izlenemedi](automation-runbook-execution.md)
* toodesign ve kullanım alt runbook'lar nasıl görürüm toounderstand [Azure Otomasyonu'nda alt runbook'lar](automation-child-runbooks.md)

