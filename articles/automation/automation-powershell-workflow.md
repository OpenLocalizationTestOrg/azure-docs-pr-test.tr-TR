---
title: "Azure otomasyonu için PowerShell iş akışı öğrenme | Microsoft Docs"
description: "Bu makalede PowerShell ve PowerShell iş akışı ve kavramları Automation runbook'larına geçerli arasındaki belirli farkları anlamak için hızlı Ders yazarlar PowerShell ile tanıdık yöneliktir."
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
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="de03c-103">Otomasyon runbook'ları için temel Windows PowerShell iş akışı kavramları öğrenme</span><span class="sxs-lookup"><span data-stu-id="de03c-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="de03c-104">Azure Otomasyonu runbook'ları Windows PowerShell iş akışları olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="de03c-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="de03c-105">Bir Windows PowerShell iş akışı, bir Windows PowerShell komut dosyası için benzer ancak yeni bir kullanıcıya kafa karıştırıcı olabilir önemli bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="de03c-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="de03c-106">Bu makale, PowerShell iş akışı kullanarak runbook'ları yazmanıza yardımcı olmak için tasarlanmıştır, ancak denetim noktaları gerekmedikçe PowerShell kullanarak runbook'ları yazma öneririz.</span><span class="sxs-lookup"><span data-stu-id="de03c-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="de03c-107">PowerShell iş akışı runbook'ları yazarken birkaç söz dizimi farkları yüklenir ve bu farklılıklar etkin iş akışları yazmak için biraz daha fazla iş gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="de03c-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="de03c-108">Bir iş akışı, uzun süre çalışan görevler gerçekleştiren veya birden fazla cihazda veya yönetilen düğümler arasında birden fazla adımın eşgüdümünü gerektiren programlı ve bağlı adımlar dizisidir.</span><span class="sxs-lookup"><span data-stu-id="de03c-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="de03c-109">Bir iş akışının normal betiğe avantajları aynı anda birden çok aygıt karşı bir eylem gerçekleştirme yeteneğini ve hatadan otomatik olarak kurtarma yeteneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="de03c-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="de03c-110">Bir Windows PowerShell iş akışı Windows Workflow Foundation kullanan bir Windows PowerShell komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="de03c-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="de03c-111">İş akışı Windows PowerShell sözdizimi kullanılarak yazılsa ve Windows PowerShell tarafından başlatılsa olsa da, Windows Workflow Foundation tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="de03c-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="de03c-112">Bu makalede konularda tam Ayrıntılar için bkz [Windows PowerShell iş akışı ile çalışmaya başlama](http://technet.microsoft.com/library/jj134242.aspx).</span><span class="sxs-lookup"><span data-stu-id="de03c-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="de03c-113">Bir iş akışının temel yapısı</span><span class="sxs-lookup"><span data-stu-id="de03c-113">Basic structure of a workflow</span></span>
<span data-ttu-id="de03c-114">Bir PowerShell iş akışı için bir PowerShell Betiği dönüştürme ilk adımı ile kapsayan **iş akışı** anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="de03c-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="de03c-115">Bir iş akışı ile başlayan **iş akışı** ayraçlar içinde betiğin gövdesi anahtar sözcüğünü.</span><span class="sxs-lookup"><span data-stu-id="de03c-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="de03c-116">İş akışının adı **iş akışı** anahtar sözcüğünü aşağıdaki sözdiziminde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="de03c-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="de03c-117">İş akışının adı Otomasyon runbook'u adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="de03c-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="de03c-118">Runbook içeri sonra dosya adı iş akışı adı ile eşleşmesi gerekir ve içinde bitmelidir *.ps1*.</span><span class="sxs-lookup"><span data-stu-id="de03c-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="de03c-119">İş akışına parametre eklemek için kullanın **Param** anahtar sözcüğü bir betik için olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="de03c-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="de03c-120">Kod değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="de03c-120">Code changes</span></span>
<span data-ttu-id="de03c-121">PowerShell iş akışı kodu birkaç önemli değişiklikler dışında bir kod PowerShell neredeyse aynı arar.</span><span class="sxs-lookup"><span data-stu-id="de03c-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="de03c-122">Aşağıdaki bölümlerde bir iş akışında çalıştırmak için bir PowerShell Betiği onun için yapmanız gereken değişiklikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="de03c-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="de03c-123">Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="de03c-123">Activities</span></span>
<span data-ttu-id="de03c-124">Bir etkinlik, bir iş akışındaki belirli bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="de03c-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="de03c-125">Yalnızca bir komut dosyası bir veya daha fazla komuttan oluşması gibi bir iş akışı etkinliklerinin sırayla gerçekleştirilen bir veya daha fazla oluşur.</span><span class="sxs-lookup"><span data-stu-id="de03c-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="de03c-126">Bir iş akışı çalıştığında, Windows PowerShell iş akışı birçok Windows PowerShell cmdlet'leri otomatik olarak etkinliklere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="de03c-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="de03c-127">Runbook'unuzda bu cmdlet'leri birini belirttiğinizde, Windows Workflow Foundation tarafından karşılık gelen etkinlik çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="de03c-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="de03c-128">Karşılık gelen bir etkinliği olmayan cmdlet'ler için Windows PowerShell iş akışı cmdlet'i otomatik olarak çalışan bir [Inlinescript](#inlinescript) etkinlik.</span><span class="sxs-lookup"><span data-stu-id="de03c-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="de03c-129">Hariç tutulan ve bir iş akışında açıkça bunları bir Inlinescript bloğunda eklemediğiniz sürece kullanılamaz cmdlet'leri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="de03c-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="de03c-130">Bu kavramlarla ilgili daha ayrıntılı bilgi için bkz: [betik iş akışlarında etkinlikleri kullanma](http://technet.microsoft.com/library/jj574194.aspx).</span><span class="sxs-lookup"><span data-stu-id="de03c-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="de03c-131">İş akışı etkinlikleri çalışmalarını yapılandıran ortak parametreler kümesini paylaşır.</span><span class="sxs-lookup"><span data-stu-id="de03c-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="de03c-132">İş akışı ortak parametreleri hakkında daha fazla ayrıntı için bkz: [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span><span class="sxs-lookup"><span data-stu-id="de03c-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="de03c-133">Konumsal Parametreler</span><span class="sxs-lookup"><span data-stu-id="de03c-133">Positional parameters</span></span>
<span data-ttu-id="de03c-134">Konumsal parametreler, etkinlikler ve iş akışı cmdlet'leri ile kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="de03c-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="de03c-135">Bunun anlamı tüm parametre adları kullanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="de03c-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="de03c-136">Örneğin, tüm çalışan hizmetler alır aşağıdaki kodu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="de03c-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="de03c-137">Bir iş akışında aynı bu kodu çalıştırmak çalışırsanız, "parametre kümesi belirtilen adlandırılmış parametreler kullanılarak çözümlenemiyor."gibi bir ileti alırsınız</span><span class="sxs-lookup"><span data-stu-id="de03c-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="de03c-138">Bu sorunu gidermek için aşağıdaki gibi parametre adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="de03c-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="de03c-139">Seri durumdan çıkarılmış nesneleri</span><span class="sxs-lookup"><span data-stu-id="de03c-139">Deserialized objects</span></span>
<span data-ttu-id="de03c-140">İş akışlarında nesneleri serisi.</span><span class="sxs-lookup"><span data-stu-id="de03c-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="de03c-141">Özellikleri hala kullanılabilir anlamına gelir, ancak bunların yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="de03c-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="de03c-142">Örneğin, hizmet nesnesinin Stop yöntemi kullanarak bir hizmet durdurur aşağıdaki PowerShell kodu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="de03c-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="de03c-143">Bu bir iş akışında çalıştırmayı denerseniz, "bir Windows PowerShell iş akışında yöntem çağırma desteklenmiyor." bildiren bir hata alıyorsunuz</span><span class="sxs-lookup"><span data-stu-id="de03c-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="de03c-144">Bir seçenektir bu iki satır kod sarmalamak için bir [Inlinescript](#inlinescript) engelle; Bu durumda $Service bloğu içinde bir hizmet nesnesi olması.</span><span class="sxs-lookup"><span data-stu-id="de03c-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="de03c-145">Başka bir seçenek varsa yöntemi aynı işlevi gerçekleştirir başka bir cmdlet kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="de03c-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="de03c-146">Bizim örnek Hizmeti Durdur cmdlet Stop yöntemi ile aynı işlevselliği sağlar ve bir iş akışı için aşağıdakileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de03c-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="de03c-147">Inlinescript</span><span class="sxs-lookup"><span data-stu-id="de03c-147">InlineScript</span></span>
<span data-ttu-id="de03c-148">**Inlinescript** etkinlik, bir veya daha fazla komutu yerine PowerShell iş akışı gibi geleneksel PowerShell betiğini çalıştırmak gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="de03c-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="de03c-149">Bir iş akışındaki komutları için Windows Workflow Foundation işleme için gönderilirken, bir Inlinescript bloğundaki komutlar Windows PowerShell tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="de03c-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="de03c-150">Inlinescript aşağıdaki aşağıdaki sözdizimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="de03c-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="de03c-151">Çıkışı bir değişkene atayarak bir Inlinescript çıkış döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="de03c-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="de03c-152">Aşağıdaki örnek, bir hizmetini durdurur ve hizmet adı çıkarır.</span><span class="sxs-lookup"><span data-stu-id="de03c-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="de03c-153">Bir Inlinescript bloğu içine değerlerinin geçmesini sağlayabilirsiniz, ancak kullanmalısınız **$Using** kapsam değiştiricisi.</span><span class="sxs-lookup"><span data-stu-id="de03c-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="de03c-154">Aşağıdaki örnek, hizmet adı değişkeni tarafından sağlanan dışında önceki örnekle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="de03c-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

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


<span data-ttu-id="de03c-155">Inlinescript etkinlikleri belirli iş akışlarında kritik olabilir, ancak iş akışı yapıları desteklemez ve yalnızca aşağıdaki nedenlerle gerekli olduğunda kullanılmalıdır:</span><span class="sxs-lookup"><span data-stu-id="de03c-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="de03c-156">Kullanamazsınız [kontrol noktaları](#checkpoints) bir Inlinescript bloğunun.</span><span class="sxs-lookup"><span data-stu-id="de03c-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="de03c-157">Blokta bir hata meydana gelirse, blok başından devam gerekir.</span><span class="sxs-lookup"><span data-stu-id="de03c-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="de03c-158">Kullanamazsınız [Paralel yürütme](#parallel-processing) bir InlineScriptBlock içinde.</span><span class="sxs-lookup"><span data-stu-id="de03c-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="de03c-159">Inlinescript bloğunun tüm uzunluğu için Windows PowerShell oturumunu tuttuğu beri Inlinescript iş akışı ölçeklenebilirliğini etkiler.</span><span class="sxs-lookup"><span data-stu-id="de03c-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="de03c-160">Inlinescript kullanma hakkında daha fazla bilgi için bkz: [bir iş akışında Windows PowerShell komutlarını çalıştırma](http://technet.microsoft.com/library/jj574197.aspx) ve [about_ınlinescript](http://technet.microsoft.com/library/jj649082.aspx).</span><span class="sxs-lookup"><span data-stu-id="de03c-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="de03c-161">Paralel işleme</span><span class="sxs-lookup"><span data-stu-id="de03c-161">Parallel processing</span></span>
<span data-ttu-id="de03c-162">Windows PowerShell iş akışlarının bir avantajı, bir komut kümesi yerine paralel sıralı olarak tipik bir betikteki gibi ile gerçekleştirmek için yeteneğidir.</span><span class="sxs-lookup"><span data-stu-id="de03c-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="de03c-163">Kullanabileceğiniz **paralel** eşzamanlı olarak çalıştıran birden çok komut içeren bir betik bloğu oluşturmak için anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="de03c-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="de03c-164">Bu, aşağıdaki aşağıdaki sözdizimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="de03c-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="de03c-165">Bu durumda, Activity1 ve Activity2 aynı anda başlar.</span><span class="sxs-lookup"><span data-stu-id="de03c-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="de03c-166">Activity3 ancak Activity1 ve Activity2 yalnızca tamamladıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="de03c-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="de03c-167">Örneğin, bir ağ hedefe birden çok dosya Kopyala aşağıdaki PowerShell komutlarını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="de03c-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="de03c-168">Sonraki başlatılmadan önce kopyalama, bir dosya bitmesi gerekir böylece bu komutlar sırayla çalışır.</span><span class="sxs-lookup"><span data-stu-id="de03c-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="de03c-169">Bunların tümü aynı anda kopyalama işlemini başlatmak için aşağıdaki iş akışı bu aynı komutları paralel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="de03c-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="de03c-170">Yalnızca tüm sonra kopyalanan tamamlama iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="de03c-170">Only after they are all copied is the completion message displayed.</span></span>

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


<span data-ttu-id="de03c-171">Kullanabileceğiniz **ForEach-Parallel** aynı anda bir koleksiyondaki her öğe için komutları işlemek üzere yapısı.</span><span class="sxs-lookup"><span data-stu-id="de03c-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="de03c-172">Betik bloğundaki komutlar sırayla yürütülürken koleksiyondaki öğeler paralel olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="de03c-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="de03c-173">Bu, aşağıdaki aşağıdaki sözdizimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="de03c-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="de03c-174">Bu durumda, Activity1 koleksiyondaki tüm öğeleri aynı anda başlar.</span><span class="sxs-lookup"><span data-stu-id="de03c-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="de03c-175">Activity1 tamamlandıktan sonra her öğe için Activity2 başlatır.</span><span class="sxs-lookup"><span data-stu-id="de03c-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="de03c-176">Activity3 ancak yalnızca tüm öğeler için Activity1 ve Activity2 tamamlandığında başlar.</span><span class="sxs-lookup"><span data-stu-id="de03c-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="de03c-177">Aşağıdaki örnek, paralel olarak dosyaları kopyalanıyor önceki örneğe benzerdir.</span><span class="sxs-lookup"><span data-stu-id="de03c-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="de03c-178">Bu durumda, onu kopyaladıktan sonra her dosya için bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="de03c-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="de03c-179">Yalnızca tüm sonra tamamen kopyaladıktan son tamamlama ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="de03c-179">Only after they are all completely copied is the final completion message displayed.</span></span>

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
> <span data-ttu-id="de03c-180">Bu güvenilir olmayan sonuçlar vermek için göstermiştir bu yana çalışan alt runbook'ları paralel olarak önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="de03c-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="de03c-181">Bazen alt runbook'tan çıkış gösterilmez ve bir alt runbook ayarlarında diğer paralel alt runbook'lar etkileyebilir</span><span class="sxs-lookup"><span data-stu-id="de03c-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="de03c-182">Kontrol noktaları</span><span class="sxs-lookup"><span data-stu-id="de03c-182">Checkpoints</span></span>
<span data-ttu-id="de03c-183">A *denetim noktası* değişkenlerin geçerli değerlerini ve bu noktaya kadar üretilen çıktıyı içerir iş akışının geçerli durumuna anlık görüntüsüdür.</span><span class="sxs-lookup"><span data-stu-id="de03c-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="de03c-184">Bir iş akışı hata sona erer veya askıya alındı, ardından İleri çalıştırıldığında, akışı başlangıcı yerine en son denetim noktasından başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="de03c-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="de03c-185">İle bir iş akışında bir denetim noktası ayarlayabilirsiniz **Checkpoint-Workflow** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="de03c-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="de03c-186">Aşağıdaki örnek kodda bir özel durum activity2 sonrasında sona erdirmek iş akışı neden olur.</span><span class="sxs-lookup"><span data-stu-id="de03c-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="de03c-187">İş akışını yeniden çalıştırdığınızda, yalnızca son denetim noktasının ayarlandığı sonra bu yana Activity2 çalıştırarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="de03c-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="de03c-188">Özel durum olabilecek ve gereken etkinliklerin iş akışı devam ettirildiğinde tekrarlanmaması sonra bir iş akışında denetim noktaları ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="de03c-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="de03c-189">Örneğin, iş akışınızı bir sanal makine oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="de03c-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="de03c-190">Önce ve sonra sanal makine oluşturma komutlarının bir denetim noktası ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de03c-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="de03c-191">Oluşturma başarısız olursa, iş akışını yeniden başlatılırsa, komutlar tekrarlar.</span><span class="sxs-lookup"><span data-stu-id="de03c-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="de03c-192">Oluşturma başarılı olduktan sonra akışı başarısız olursa, iş akışı sürdürüldüğünde sonra sanal makineyi yeniden oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="de03c-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="de03c-193">Aşağıdaki örnek, birden çok dosyalarını bir ağ konumuna kopyalar ve sonra her bir dosyanın bir denetim noktası ayarlar.</span><span class="sxs-lookup"><span data-stu-id="de03c-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="de03c-194">Ağ konumu kaybolursa, iş akışı hata sona erer.</span><span class="sxs-lookup"><span data-stu-id="de03c-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="de03c-195">Yeniden başlatıldığında, önceden kopyaladığınız dosyalar atlanır anlamı son denetim noktası devam eder.</span><span class="sxs-lookup"><span data-stu-id="de03c-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="de03c-196">Çağırdıktan sonra kullanıcı adı kimlik bilgilerini kalıcı değildir çünkü [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) etkinlik veya null ve sonra bunları yeniden sonra varlık deposundan almak için kimlik bilgilerini ayarlamak gereken en son kontrol sonra  **Suspend-Workflow** ya da kontrol noktası çağrılır.</span><span class="sxs-lookup"><span data-stu-id="de03c-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="de03c-197">Aksi takdirde, aşağıdaki hata iletisini alabilirsiniz: *iş akışının devam ettirilemez, Kalıcılık veri bırakılamadı tamamen kaydedildi, veya kaydedilen çünkü kalıcı veri ya da bozulmuş. İş akışını yeniden başlatmanız gerekir.*</span><span class="sxs-lookup"><span data-stu-id="de03c-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="de03c-198">Aşağıdaki aynı kod bu PowerShell iş akışı larınızda nasıl ele alınacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="de03c-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="de03c-199">Hizmet sorumlusu ile yapılandırılmış olan bir farklı çalıştır hesabını kullanarak kimlik doğrulaması yaptıklarını, bu gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="de03c-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="de03c-200">Kontrol noktaları hakkında daha fazla bilgi için bkz: [betik iş akışına denetim noktaları ekleme](http://technet.microsoft.com/library/jj574114.aspx).</span><span class="sxs-lookup"><span data-stu-id="de03c-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de03c-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de03c-201">Next steps</span></span>
* <span data-ttu-id="de03c-202">PowerShell iş akışı runbook'larını kullanmaya başlamak için bkz. [İlk PowerShell iş akışı runbook uygulamam](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="de03c-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
