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
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="5264f-103">Otomasyon runbook'ları için temel Windows PowerShell iş akışı kavramları öğrenme</span><span class="sxs-lookup"><span data-stu-id="5264f-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="5264f-104">Azure Otomasyonu runbook'ları Windows PowerShell iş akışları olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5264f-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="5264f-105">Bir Windows PowerShell iş akışı benzer tooa Windows PowerShell komut dosyası ancak kafa karıştırıcı tooa yeni kullanıcı olabilecek önemli farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="5264f-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="5264f-106">Bu makalede PowerShell iş akışı kullanarak runbook'ları yazma hedeflenen toohelp olsa da, denetim noktaları gerekmedikçe PowerShell kullanarak runbook'ları yazma öneririz.</span><span class="sxs-lookup"><span data-stu-id="5264f-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="5264f-107">PowerShell iş akışı runbook'ları yazarken birkaç söz dizimi farkları yüklenir ve bu farklılıklar biraz daha fazla iş toowrite etkin iş akışı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="5264f-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="5264f-108">Bir iş akışı, uzun süre çalışan görevler gerçekleştiren veya birden fazla cihazda veya yönetilen düğümler arasında hello birden fazla adımın eşgüdümünü gerektiren programlı ve bağlı adımlar dizisidir.</span><span class="sxs-lookup"><span data-stu-id="5264f-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="5264f-109">Merhaba bir iş akışının normal betiğe hello özelliği yararları toosimultaneously birden çok aygıt karşı bir eylemi gerçekleştirir ve hello özelliği tooautomatically hatalarından kurtarın.</span><span class="sxs-lookup"><span data-stu-id="5264f-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="5264f-110">Bir Windows PowerShell iş akışı Windows Workflow Foundation kullanan bir Windows PowerShell komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5264f-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="5264f-111">Merhaba iş akışı Windows PowerShell sözdizimi kullanılarak yazılsa ve Windows PowerShell tarafından başlatılsa olsa da, Windows Workflow Foundation tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="5264f-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="5264f-112">Bu makalede hello konularda tam Ayrıntılar için bkz [Windows PowerShell iş akışı ile çalışmaya başlama](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="5264f-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="5264f-113">Bir iş akışının temel yapısı</span><span class="sxs-lookup"><span data-stu-id="5264f-113">Basic structure of a workflow</span></span>
<span data-ttu-id="5264f-114">Merhaba ilk adım tooconverting bir PowerShell komut dosyası tooa PowerShell iş akışı, ile Merhaba kapsayan **iş akışı** anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="5264f-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="5264f-115">Bir iş akışı ile Merhaba başlatır **iş akışı** hello ayraçlar içinde hello betik gövdesi arkasından anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="5264f-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="5264f-116">Merhaba iş akışının Hello adından sonra hello **iş akışı** hello sözdizimi aşağıdaki gösterildiği gibi anahtar sözcüğü:</span><span class="sxs-lookup"><span data-stu-id="5264f-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="5264f-117">Hello hello iş akışı hello Otomasyon runbook'u hello adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="5264f-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="5264f-118">Merhaba runbook alınmakta sonra hello filename hello iş akışı adıyla eşleşmelidir ve sonunda *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="5264f-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="5264f-119">tooadd parametreleri toohello iş akışı, kullanım hello **Param** anahtar sözcüğü tooa betik olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="5264f-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="5264f-120">Kod değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="5264f-120">Code changes</span></span>
<span data-ttu-id="5264f-121">PowerShell iş akışı kodu birkaç önemli değişiklikler dışında bir kod neredeyse aynı tooPowerShell arar.</span><span class="sxs-lookup"><span data-stu-id="5264f-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="5264f-122">Aşağıdaki bölümlerde hello bir iş akışında toorun için toomake tooa PowerShell Betiği gereken değişiklikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="5264f-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="5264f-123">Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="5264f-123">Activities</span></span>
<span data-ttu-id="5264f-124">Bir etkinlik, bir iş akışındaki belirli bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="5264f-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="5264f-125">Yalnızca bir komut dosyası bir veya daha fazla komuttan oluşması gibi bir iş akışı etkinliklerinin sırayla gerçekleştirilen bir veya daha fazla oluşur.</span><span class="sxs-lookup"><span data-stu-id="5264f-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="5264f-126">Bir iş akışı çalıştığında, Windows PowerShell iş akışı otomatik olarak birçok hello Windows PowerShell cmdlet'leri tooactivities dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="5264f-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="5264f-127">Runbook'unuzda bu cmdlet'leri birini belirttiğinizde, Windows Workflow Foundation tarafından hello karşılık gelen etkinlik çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5264f-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="5264f-128">Karşılık gelen bir etkinliği olmayan cmdlet'ler için Windows PowerShell iş akışı içinde hello cmdlet'i otomatik olarak çalıştırır bir [Inlinescript](#inlinescript) etkinlik.</span><span class="sxs-lookup"><span data-stu-id="5264f-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="5264f-129">Hariç tutulan ve bir iş akışında açıkça bunları bir Inlinescript bloğunda eklemediğiniz sürece kullanılamaz cmdlet'leri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="5264f-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="5264f-130">Bu kavramlarla ilgili daha ayrıntılı bilgi için bkz: [betik iş akışlarında etkinlikleri kullanma](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="5264f-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="5264f-131">İş akışı etkinlikleri çalışmalarını ortak parametreleri tooconfigure kümesini paylaşır.</span><span class="sxs-lookup"><span data-stu-id="5264f-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="5264f-132">Merhaba iş akışı ortak parametreleri hakkında daha fazla ayrıntı için bkz: [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="5264f-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="5264f-133">Konumsal Parametreler</span><span class="sxs-lookup"><span data-stu-id="5264f-133">Positional parameters</span></span>
<span data-ttu-id="5264f-134">Konumsal parametreler, etkinlikler ve iş akışı cmdlet'leri ile kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="5264f-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="5264f-135">Bunun anlamı tüm parametre adları kullanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="5264f-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="5264f-136">Örneğin, tüm çalışan hizmetler alır koddan hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5264f-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="5264f-137">Bir iş akışı aynı bu kodda toorun çalışırsanız, "parametreleri adlı parametre kümesi belirtilen hello kullanılarak çözümlenemiyor."gibi bir ileti alırsınız</span><span class="sxs-lookup"><span data-stu-id="5264f-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="5264f-138">toocorrect bunu hello aşağıdaki gibi hello parametre adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5264f-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="5264f-139">Seri durumdan çıkarılmış nesneleri</span><span class="sxs-lookup"><span data-stu-id="5264f-139">Deserialized objects</span></span>
<span data-ttu-id="5264f-140">İş akışlarında nesneleri serisi.</span><span class="sxs-lookup"><span data-stu-id="5264f-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="5264f-141">Özellikleri hala kullanılabilir anlamına gelir, ancak bunların yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="5264f-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="5264f-142">Örneğin, hello hizmeti nesnesinin hello Stop yöntemi kullanarak bir hizmet durdurur PowerShell kodu aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5264f-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="5264f-143">Toorun bu bir iş akışında denerseniz, "bir Windows PowerShell iş akışında yöntem çağırma desteklenmiyor." bildiren bir hata alıyorsunuz</span><span class="sxs-lookup"><span data-stu-id="5264f-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="5264f-144">Bir seçenektir toowrap bu iki satır kod bir [Inlinescript](#inlinescript) engelle; Bu durumda $Service hello bloğu içinde bir hizmet nesnesi olması.</span><span class="sxs-lookup"><span data-stu-id="5264f-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="5264f-145">Başka bir seçenektir toouse gerçekleştirir başka bir cmdlet hello hello yöntemi aynı işlevselliği varsa.</span><span class="sxs-lookup"><span data-stu-id="5264f-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="5264f-146">Bizim örnek hello Hizmeti Durdur cmdlet hello sağlar hello durdurma yöntemi ve aynı işlevselliği hello aşağıdaki iş akışı için kullanır.</span><span class="sxs-lookup"><span data-stu-id="5264f-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="5264f-147">Inlinescript</span><span class="sxs-lookup"><span data-stu-id="5264f-147">InlineScript</span></span>
<span data-ttu-id="5264f-148">Merhaba **Inlinescript** etkinlik, PowerShell iş akışı yerine geleneksel PowerShell Betiği olarak bir veya daha fazla komut toorun ihtiyacınız olduğunda yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="5264f-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="5264f-149">Bir iş akışındaki komutları tooWindows Workflow Foundation işleme için gönderilirken, bir Inlinescript bloğundaki komutlar Windows PowerShell tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="5264f-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="5264f-150">Inlinescript aşağıda gösterilen sözdizimi aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="5264f-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="5264f-151">Merhaba çıktı tooa değişkeni atayarak bir Inlinescript çıkış döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="5264f-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="5264f-152">Merhaba aşağıdaki örnekte bir hizmetini durdurur ve hello hizmet adı çıkarır.</span><span class="sxs-lookup"><span data-stu-id="5264f-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="5264f-153">Bir Inlinescript bloğu içine değerlerinin geçmesini sağlayabilirsiniz, ancak kullanmalısınız **$Using** kapsam değiştiricisi.</span><span class="sxs-lookup"><span data-stu-id="5264f-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="5264f-154">Merhaba hizmet adı değişkeni tarafından sağlanan hello aşağıdaki örnek aynı toohello önceki örnek olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="5264f-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

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


<span data-ttu-id="5264f-155">Inlinescript etkinlikleri belirli iş akışlarında kritik olabilir, ancak iş akışı yapıları desteklemez ve yalnızca aşağıdaki nedenlerle hello için gerekli olduğunda kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="5264f-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="5264f-156">Kullanamazsınız [kontrol noktaları](#checkpoints) bir Inlinescript bloğunun.</span><span class="sxs-lookup"><span data-stu-id="5264f-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="5264f-157">Merhaba blokta bir hata meydana gelirse, hello hello blok başından devam gerekir.</span><span class="sxs-lookup"><span data-stu-id="5264f-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="5264f-158">Kullanamazsınız [Paralel yürütme](#parallel-processing) bir InlineScriptBlock içinde.</span><span class="sxs-lookup"><span data-stu-id="5264f-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="5264f-159">Hello Inlinescript bloğunun tüm uzunluğu hello hello Windows PowerShell oturumunu tuttuğu beri Inlinescript hello iş akışı ölçeklenebilirliğini etkiler.</span><span class="sxs-lookup"><span data-stu-id="5264f-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="5264f-160">Inlinescript kullanma hakkında daha fazla bilgi için bkz: [bir iş akışında Windows PowerShell komutlarını çalıştırma](http://technet.microsoft.com/library/jj574197.aspx) ve [about_ınlinescript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="5264f-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="5264f-161">Paralel işleme</span><span class="sxs-lookup"><span data-stu-id="5264f-161">Parallel processing</span></span>
<span data-ttu-id="5264f-162">Windows PowerShell iş akışlarının bir avantajı hello özelliği tooperform komutları yerine paralel sıralı olarak tipik bir betikteki gibi ile kümesidir.</span><span class="sxs-lookup"><span data-stu-id="5264f-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="5264f-163">Merhaba kullanabilirsiniz **paralel** anahtar sözcüğü toocreate eşzamanlı olarak çalışan birden çok komutlar ile bir betik bloğu.</span><span class="sxs-lookup"><span data-stu-id="5264f-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="5264f-164">Bu, aşağıda gösterilen sözdizimi aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="5264f-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="5264f-165">Bu durumda, Activity1 ve Activity2 başlar hello aynı anda.</span><span class="sxs-lookup"><span data-stu-id="5264f-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="5264f-166">Activity3 ancak Activity1 ve Activity2 yalnızca tamamladıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="5264f-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="5264f-167">Örneğin, birden çok dosya tooa Ağ hedefi Kopyala PowerShell komutlarını aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5264f-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="5264f-168">Bu bir dosyayı hello sonraki başlatılmadan önce kopyalama bitmesi gerekir böylece bu komutlar sıralı olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5264f-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="5264f-169">Merhaba aşağıdaki iş akışı bunları aynı komutları paralel olarak hepsi aynı hello kopyalama başlatılması çalıştırır zaman.</span><span class="sxs-lookup"><span data-stu-id="5264f-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="5264f-170">Yalnızca tüm sonra kopyalanan hello tamamlama iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5264f-170">Only after they are all copied is hello completion message displayed.</span></span>

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


<span data-ttu-id="5264f-171">Merhaba kullanabilirsiniz **ForEach-Parallel** tooprocess bir koleksiyondaki her öğe için komutları eşzamanlı olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5264f-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="5264f-172">Merhaba hello betik bloğundaki komutlar sırayla yürütülürken hello koleksiyonundaki hello öğeler paralel olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="5264f-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="5264f-173">Bu, aşağıda gösterilen sözdizimi aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="5264f-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="5264f-174">Bu durumda, Activity1 başlar hello aynı hello koleksiyondaki tüm öğeleri zaman.</span><span class="sxs-lookup"><span data-stu-id="5264f-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="5264f-175">Activity1 tamamlandıktan sonra her öğe için Activity2 başlatır.</span><span class="sxs-lookup"><span data-stu-id="5264f-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="5264f-176">Activity3 ancak yalnızca tüm öğeler için Activity1 ve Activity2 tamamlandığında başlar.</span><span class="sxs-lookup"><span data-stu-id="5264f-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="5264f-177">Aşağıdaki örneğine hello paralel olarak dosyaları kopyalanıyor benzer toohello önceki bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="5264f-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="5264f-178">Bu durumda, onu kopyaladıktan sonra her dosya için bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5264f-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="5264f-179">Yalnızca tüm sonra tamamen kopyaladıktan hello son tamamlama ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5264f-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

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
> <span data-ttu-id="5264f-180">Bu toogive güvenilir olmayan sonuçlar gösterilen olduğundan, alt runbook'ları paralel olarak çalışan önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5264f-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="5264f-181">Merhaba bazen hello alt runbook'un çıktısını görünmez ve bir alt runbook ayarlarında etkileyebilecek diğer paralel alt runbook'ları hello</span><span class="sxs-lookup"><span data-stu-id="5264f-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="5264f-182">Kontrol noktaları</span><span class="sxs-lookup"><span data-stu-id="5264f-182">Checkpoints</span></span>
<span data-ttu-id="5264f-183">A *denetim noktası* iş akışının hello değişkenlerin geçerli değerlerini içeren hello hello geçerli durumunun bir anlık görüntüdür ve herhangi bir oluşturulan toothat noktası çıktı.</span><span class="sxs-lookup"><span data-stu-id="5264f-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="5264f-184">Bir iş akışı hata sona erer veya askıya alındı, hello hello akışı hello başlangıcı yerine en son denetim noktasından onu İleri çalıştırıldığında başlatılır.</span><span class="sxs-lookup"><span data-stu-id="5264f-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="5264f-185">Merhaba ile bir iş akışında bir denetim noktası ayarlayabilirsiniz **Checkpoint-Workflow** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="5264f-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="5264f-186">Activity2 neden hello sonra iş akışı tooend hello aşağıdaki örnek kod, bir özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="5264f-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="5264f-187">Merhaba iş akışını yeniden çalıştırdığınızda, yalnızca en son kontrol hello ayarladıktan sonra bu yana Activity2 çalıştırarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="5264f-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="5264f-188">Yatkın tooexception olabilir ve olmamalıdır etkinlikleri hello iş akışı devam ettirildiğinde tekrarlanmaması sonra bir iş akışında denetim noktaları ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5264f-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="5264f-189">Örneğin, iş akışınızı bir sanal makine oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="5264f-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="5264f-190">Öncesinde ve sonrasında hello komutları toocreate hello sanal makine bir denetim noktası ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5264f-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="5264f-191">Merhaba oluşturma başarısız olursa hello iş akışı yeniden başlatılırsa, ardından hello komutları yinelenmesi.</span><span class="sxs-lookup"><span data-stu-id="5264f-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="5264f-192">Merhaba oluşturma başarılı olduktan sonra hello akışı başarısız olursa, hello iş akışı sürdürüldüğünde sonra hello sanal makine yeniden oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="5264f-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="5264f-193">Aşağıdaki örneğine hello birden çok dosya tooa ağ konumuna kopyalar ve sonra her bir dosyanın bir denetim noktası ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5264f-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="5264f-194">Merhaba ağ konumu kaybolursa, hello iş akışı hata sona erer.</span><span class="sxs-lookup"><span data-stu-id="5264f-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="5264f-195">Yeniden başlatıldığında, önceden kopyaladığınız hello dosyalar atlanır anlamı hello son denetim noktası devam eder.</span><span class="sxs-lookup"><span data-stu-id="5264f-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="5264f-196">Merhaba çağırdıktan sonra kullanıcı adı kimlik bilgilerini kalıcı değildir çünkü [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) etkinlik veya hello en son kontrol sonra tooset hello kimlik bilgileri toonull gerekir ve sonra bunları yeniden hello varlık Mağaza'dan sonra alır **Suspend-Workflow** ya da kontrol noktası çağrılır.</span><span class="sxs-lookup"><span data-stu-id="5264f-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="5264f-197">Aksi takdirde hello aşağıdaki hata iletisini alabilirsiniz: *hello iş akışı tanımlı işlemi yapamazsınız sürdürüldü, Kalıcılık veri bırakılamadı tamamen kaydedildi, veya kaydedilen çünkü kalıcı veri ya da bozulmuş. Merhaba iş akışını yeniden başlatmanız gerekir.*</span><span class="sxs-lookup"><span data-stu-id="5264f-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="5264f-198">aynı koddan hello gösteren nasıl toohandle bu PowerShell iş akışı runbook'larınızdaki.</span><span class="sxs-lookup"><span data-stu-id="5264f-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

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


<span data-ttu-id="5264f-199">Hizmet sorumlusu ile yapılandırılmış olan bir farklı çalıştır hesabını kullanarak kimlik doğrulaması yaptıklarını, bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="5264f-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="5264f-200">Kontrol noktaları hakkında daha fazla bilgi için bkz: [komut dosyası iş akışına denetim noktaları ekleme tooa](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="5264f-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5264f-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5264f-201">Next steps</span></span>
* <span data-ttu-id="5264f-202">PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="5264f-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
