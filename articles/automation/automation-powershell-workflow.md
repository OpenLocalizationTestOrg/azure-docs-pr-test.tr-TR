---
title: "Azure otomasyonu için PowerShell iş akışı aaaLearning | Microsoft Docs"
description: "Bu makalede Hızlı Ders yazarlar PowerShell toounderstand hello belirli farklılıklar PowerShell ve PowerShell iş akışı ve kavramları geçerli tooAutomation runbook'lar arasında aşina yöneliktir."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>Otomasyon runbook'ları için temel Windows PowerShell iş akışı kavramları öğrenme 
Azure Otomasyonu runbook'ları Windows PowerShell iş akışları olarak uygulanır.  Bir Windows PowerShell iş akışı benzer tooa Windows PowerShell komut dosyası ancak kafa karıştırıcı tooa yeni kullanıcı olabilecek önemli farklılıklar vardır.  Bu makalede PowerShell iş akışı kullanarak runbook'ları yazma hedeflenen toohelp olsa da, denetim noktaları gerekmedikçe PowerShell kullanarak runbook'ları yazma öneririz.  PowerShell iş akışı runbook'ları yazarken birkaç söz dizimi farkları yüklenir ve bu farklılıklar biraz daha fazla iş toowrite etkin iş akışı gerektirmez.  

Bir iş akışı, uzun süre çalışan görevler gerçekleştiren veya birden fazla cihazda veya yönetilen düğümler arasında hello birden fazla adımın eşgüdümünü gerektiren programlı ve bağlı adımlar dizisidir. Merhaba bir iş akışının normal betiğe hello özelliği yararları toosimultaneously birden çok aygıt karşı bir eylemi gerçekleştirir ve hello özelliği tooautomatically hatalarından kurtarın. Bir Windows PowerShell iş akışı Windows Workflow Foundation kullanan bir Windows PowerShell komut dosyasıdır. Merhaba iş akışı Windows PowerShell sözdizimi kullanılarak yazılsa ve Windows PowerShell tarafından başlatılsa olsa da, Windows Workflow Foundation tarafından işlenir.

Bu makalede hello konularda tam Ayrıntılar için bkz [Windows PowerShell iş akışı ile çalışmaya başlama](http://technet.microsoft.com/library/jj134242.aspx).

## <a name="basic-structure-of-a-workflow"></a>Bir iş akışının temel yapısı
Merhaba ilk adım tooconverting bir PowerShell komut dosyası tooa PowerShell iş akışı, ile Merhaba kapsayan **iş akışı** anahtar sözcüğü.  Bir iş akışı ile Merhaba başlatır **iş akışı** hello ayraçlar içinde hello betik gövdesi arkasından anahtar sözcüğü. Merhaba iş akışının Hello adından sonra hello **iş akışı** hello sözdizimi aşağıdaki gösterildiği gibi anahtar sözcüğü:

    Workflow Test-Workflow
    {
       <Commands>
    }

Hello hello iş akışı hello Otomasyon runbook'u hello adı eşleşmelidir. Merhaba runbook alınmakta sonra hello filename hello iş akışı adıyla eşleşmelidir ve sonunda *.ps1*.

tooadd parametreleri toohello iş akışı, kullanım hello **Param** anahtar sözcüğü tooa betik olduğu gibi.

## <a name="code-changes"></a>Kod değişiklikleri
PowerShell iş akışı kodu birkaç önemli değişiklikler dışında bir kod neredeyse aynı tooPowerShell arar.  Aşağıdaki bölümlerde hello bir iş akışında toorun için toomake tooa PowerShell Betiği gereken değişiklikleri açıklar.

### <a name="activities"></a>Etkinlikler
Bir etkinlik, bir iş akışındaki belirli bir görevdir. Yalnızca bir komut dosyası bir veya daha fazla komuttan oluşması gibi bir iş akışı etkinliklerinin sırayla gerçekleştirilen bir veya daha fazla oluşur. Bir iş akışı çalıştığında, Windows PowerShell iş akışı otomatik olarak birçok hello Windows PowerShell cmdlet'leri tooactivities dönüştürür. Runbook'unuzda bu cmdlet'leri birini belirttiğinizde, Windows Workflow Foundation tarafından hello karşılık gelen etkinlik çalıştırılır. Karşılık gelen bir etkinliği olmayan cmdlet'ler için Windows PowerShell iş akışı içinde hello cmdlet'i otomatik olarak çalıştırır bir [Inlinescript](#inlinescript) etkinlik. Hariç tutulan ve bir iş akışında açıkça bunları bir Inlinescript bloğunda eklemediğiniz sürece kullanılamaz cmdlet'leri kümesi yok. Bu kavramlarla ilgili daha ayrıntılı bilgi için bkz: [betik iş akışlarında etkinlikleri kullanma](http://technet.microsoft.com/library/jj574194.aspx).

İş akışı etkinlikleri çalışmalarını ortak parametreleri tooconfigure kümesini paylaşır. Merhaba iş akışı ortak parametreleri hakkında daha fazla ayrıntı için bkz: [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).

### <a name="positional-parameters"></a>Konumsal Parametreler
Konumsal parametreler, etkinlikler ve iş akışı cmdlet'leri ile kullanamazsınız.  Bunun anlamı tüm parametre adları kullanmasıdır.

Örneğin, tüm çalışan hizmetler alır koddan hello göz önünde bulundurun.

     Get-Service | Where-Object {$_.Status -eq "Running"}

Bir iş akışı aynı bu kodda toorun çalışırsanız, "parametreleri adlı parametre kümesi belirtilen hello kullanılarak çözümlenemiyor."gibi bir ileti alırsınız  toocorrect bunu hello aşağıdaki gibi hello parametre adı sağlayın.

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>Seri durumdan çıkarılmış nesneleri
İş akışlarında nesneleri serisi.  Özellikleri hala kullanılabilir anlamına gelir, ancak bunların yöntemleri.  Örneğin, hello hizmeti nesnesinin hello Stop yöntemi kullanarak bir hizmet durdurur PowerShell kodu aşağıdaki hello göz önünde bulundurun.

    $Service = Get-Service -Name MyService
    $Service.Stop()

Toorun bu bir iş akışında denerseniz, "bir Windows PowerShell iş akışında yöntem çağırma desteklenmiyor." bildiren bir hata alıyorsunuz  

Bir seçenektir toowrap bu iki satır kod bir [Inlinescript](#inlinescript) engelle; Bu durumda $Service hello bloğu içinde bir hizmet nesnesi olması.

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

Başka bir seçenektir toouse gerçekleştirir başka bir cmdlet hello hello yöntemi aynı işlevselliği varsa.  Bizim örnek hello Hizmeti Durdur cmdlet hello sağlar hello durdurma yöntemi ve aynı işlevselliği hello aşağıdaki iş akışı için kullanır.

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>Inlinescript
Merhaba **Inlinescript** etkinlik, PowerShell iş akışı yerine geleneksel PowerShell Betiği olarak bir veya daha fazla komut toorun ihtiyacınız olduğunda yararlıdır.  Bir iş akışındaki komutları tooWindows Workflow Foundation işleme için gönderilirken, bir Inlinescript bloğundaki komutlar Windows PowerShell tarafından işlenir.

Inlinescript aşağıda gösterilen sözdizimi aşağıdaki hello kullanır.

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

Merhaba çıktı tooa değişkeni atayarak bir Inlinescript çıkış döndürebilir. Merhaba aşağıdaki örnekte bir hizmetini durdurur ve hello hizmet adı çıkarır.

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Bir Inlinescript bloğu içine değerlerinin geçmesini sağlayabilirsiniz, ancak kullanmalısınız **$Using** kapsam değiştiricisi.  Merhaba hizmet adı değişkeni tarafından sağlanan hello aşağıdaki örnek aynı toohello önceki örnek olmasıdır.

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


Inlinescript etkinlikleri belirli iş akışlarında kritik olabilir, ancak iş akışı yapıları desteklemez ve yalnızca aşağıdaki nedenlerle hello için gerekli olduğunda kullanılmalıdır:

* Kullanamazsınız [kontrol noktaları](#checkpoints) bir Inlinescript bloğunun. Merhaba blokta bir hata meydana gelirse, hello hello blok başından devam gerekir.
* Kullanamazsınız [Paralel yürütme](#parallel-processing) bir InlineScriptBlock içinde.
* Hello Inlinescript bloğunun tüm uzunluğu hello hello Windows PowerShell oturumunu tuttuğu beri Inlinescript hello iş akışı ölçeklenebilirliğini etkiler.

Inlinescript kullanma hakkında daha fazla bilgi için bkz: [bir iş akışında Windows PowerShell komutlarını çalıştırma](http://technet.microsoft.com/library/jj574197.aspx) ve [about_ınlinescript](http://technet.microsoft.com/library/jj649082.aspx).

## <a name="parallel-processing"></a>Paralel işleme
Windows PowerShell iş akışlarının bir avantajı hello özelliği tooperform komutları yerine paralel sıralı olarak tipik bir betikteki gibi ile kümesidir.

Merhaba kullanabilirsiniz **paralel** anahtar sözcüğü toocreate eşzamanlı olarak çalışan birden çok komutlar ile bir betik bloğu. Bu, aşağıda gösterilen sözdizimi aşağıdaki hello kullanır. Bu durumda, Activity1 ve Activity2 başlar hello aynı anda. Activity3 ancak Activity1 ve Activity2 yalnızca tamamladıktan sonra başlar.

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


Örneğin, birden çok dosya tooa Ağ hedefi Kopyala PowerShell komutlarını aşağıdaki hello göz önünde bulundurun.  Bu bir dosyayı hello sonraki başlatılmadan önce kopyalama bitmesi gerekir böylece bu komutlar sıralı olarak çalıştırılır.     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

Merhaba aşağıdaki iş akışı bunları aynı komutları paralel olarak hepsi aynı hello kopyalama başlatılması çalıştırır zaman.  Yalnızca tüm sonra kopyalanan hello tamamlama iletisi görüntülenir.

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


Merhaba kullanabilirsiniz **ForEach-Parallel** tooprocess bir koleksiyondaki her öğe için komutları eşzamanlı olarak oluşturun. Merhaba hello betik bloğundaki komutlar sırayla yürütülürken hello koleksiyonundaki hello öğeler paralel olarak işlenir. Bu, aşağıda gösterilen sözdizimi aşağıdaki hello kullanır. Bu durumda, Activity1 başlar hello aynı hello koleksiyondaki tüm öğeleri zaman. Activity1 tamamlandıktan sonra her öğe için Activity2 başlatır. Activity3 ancak yalnızca tüm öğeler için Activity1 ve Activity2 tamamlandığında başlar.

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

Aşağıdaki örneğine hello paralel olarak dosyaları kopyalanıyor benzer toohello önceki bir örnektir.  Bu durumda, onu kopyaladıktan sonra her dosya için bir ileti görüntülenir.  Yalnızca tüm sonra tamamen kopyaladıktan hello son tamamlama ileti görüntülenir.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> Bu toogive güvenilir olmayan sonuçlar gösterilen olduğundan, alt runbook'ları paralel olarak çalışan önermiyoruz.  Merhaba bazen hello alt runbook'un çıktısını görünmez ve bir alt runbook ayarlarında etkileyebilecek diğer paralel alt runbook'ları hello
>

## <a name="checkpoints"></a>Kontrol noktaları
A *denetim noktası* iş akışının hello değişkenlerin geçerli değerlerini içeren hello hello geçerli durumunun bir anlık görüntüdür ve herhangi bir oluşturulan toothat noktası çıktı. Bir iş akışı hata sona erer veya askıya alındı, hello hello akışı hello başlangıcı yerine en son denetim noktasından onu İleri çalıştırıldığında başlatılır.  Merhaba ile bir iş akışında bir denetim noktası ayarlayabilirsiniz **Checkpoint-Workflow** etkinlik.

Activity2 neden hello sonra iş akışı tooend hello aşağıdaki örnek kod, bir özel durum oluşur. Merhaba iş akışını yeniden çalıştırdığınızda, yalnızca en son kontrol hello ayarladıktan sonra bu yana Activity2 çalıştırarak başlatır.

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

Yatkın tooexception olabilir ve olmamalıdır etkinlikleri hello iş akışı devam ettirildiğinde tekrarlanmaması sonra bir iş akışında denetim noktaları ayarlamanız gerekir. Örneğin, iş akışınızı bir sanal makine oluşturabilir. Öncesinde ve sonrasında hello komutları toocreate hello sanal makine bir denetim noktası ayarlayabilirsiniz. Merhaba oluşturma başarısız olursa hello iş akışı yeniden başlatılırsa, ardından hello komutları yinelenmesi. Merhaba oluşturma başarılı olduktan sonra hello akışı başarısız olursa, hello iş akışı sürdürüldüğünde sonra hello sanal makine yeniden oluşturulmaz.

Aşağıdaki örneğine hello birden çok dosya tooa ağ konumuna kopyalar ve sonra her bir dosyanın bir denetim noktası ayarlar.  Merhaba ağ konumu kaybolursa, hello iş akışı hata sona erer.  Yeniden başlatıldığında, önceden kopyaladığınız hello dosyalar atlanır anlamı hello son denetim noktası devam eder.

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

Merhaba çağırdıktan sonra kullanıcı adı kimlik bilgilerini kalıcı değildir çünkü [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) etkinlik veya hello en son kontrol sonra tooset hello kimlik bilgileri toonull gerekir ve sonra bunları yeniden hello varlık Mağaza'dan sonra alır **Suspend-Workflow** ya da kontrol noktası çağrılır.  Aksi takdirde hello aşağıdaki hata iletisini alabilirsiniz: *hello iş akışı tanımlı işlemi yapamazsınız sürdürüldü, Kalıcılık veri bırakılamadı tamamen kaydedildi, veya kaydedilen çünkü kalıcı veri ya da bozulmuş. Merhaba iş akışını yeniden başlatmanız gerekir.*

aynı koddan hello gösteren nasıl toohandle bu PowerShell iş akışı runbook'larınızdaki.

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


Hizmet sorumlusu ile yapılandırılmış olan bir farklı çalıştır hesabını kullanarak kimlik doğrulaması yaptıklarını, bu gerekli değildir.  

Kontrol noktaları hakkında daha fazla bilgi için bkz: [komut dosyası iş akışına denetim noktaları ekleme tooa](http://technet.microsoft.com/library/jj574114.aspx).

## <a name="next-steps"></a>Sonraki adımlar
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)
