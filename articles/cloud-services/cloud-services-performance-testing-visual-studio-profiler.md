---
title: "bir bulut hizmeti yerel olarak hello işlem öykünücüsü içinde aaaProfiling | Microsoft Docs"
services: cloud-services
description: "Merhaba Visual Studio Profil Oluşturucu ile bulut Hizmetleri performans sorunları araştırmak"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="6242d-103">Hello Azure işlem öykünücüsü kullanarak hello Visual Studio profil oluşturucu Hello performansını bir bulut hizmeti yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="6242d-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="6242d-104">Çeşitli araçları ve teknikleri, bulut Hizmetleri hello performansını test etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6242d-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="6242d-105">Bir bulut hizmeti tooAzure yayımladığınızda, Visual Studio profil oluşturma verileri toplamak ve ardından analiz olabilir açıklandığı gibi yerel olarak [bir Azure uygulama profili oluşturma][1].</span><span class="sxs-lookup"><span data-stu-id="6242d-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="6242d-106">De açıklandığı gibi çeşitli performans sayaçları, tanılama tootrack kullanabilirsiniz [Azure'da performans sayaçlarını kullanarak][2].</span><span class="sxs-lookup"><span data-stu-id="6242d-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="6242d-107">Tooprofile toohello bulut dağıtmadan önce uygulamanızda yerel olarak hello işlem öykünücüsü isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="6242d-108">Bu makalede, yerel olarak hello öykünücüsünde yapılabilir profil hello CPU örnekleme yöntemi kapsar.</span><span class="sxs-lookup"><span data-stu-id="6242d-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="6242d-109">CPU örnekleme, profil oluşturma yöntemi çok zorlayıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="6242d-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="6242d-110">Belirlenen örnekleme aralığı sırasında hello profil oluşturucu hello çağrı yığınının bir anlık görüntüsünü alır.</span><span class="sxs-lookup"><span data-stu-id="6242d-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="6242d-111">Merhaba veriler, bir süre boyunca toplanan ve bir raporda.</span><span class="sxs-lookup"><span data-stu-id="6242d-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="6242d-112">Profil oluşturma yöntemi, burada bir pkı'ya yoğun uygulamasında hello CPU çalışmanın çoğu yapılır tooindicate eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="6242d-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="6242d-113">Bu, uygulamanızın çoğu zaman hello yeri harcıyorsa fırsat toofocus yolunda hello"etkin" Merhaba olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6242d-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="6242d-114">1: profil oluşturma için Visual Studio'yu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6242d-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="6242d-115">İlk olarak, profil oluşturma zaman yararlı olabilecek birkaç Visual Studio yapılandırma seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="6242d-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="6242d-116">toomake duygusu hello profil oluşturma raporları, uygulama ve ayrıca sistem kitaplıkları simgelerini simge (.pdb dosyaları) gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242d-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="6242d-117">Toomake hello kullanılabilir simge sunucuları başvuru emin isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="6242d-118">toodo hello üzerinde bu **Araçları** Visual Studio'da menüsünü seçin **seçenekleri**, ardından **hata ayıklama**, sonra **simgeleri**.</span><span class="sxs-lookup"><span data-stu-id="6242d-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="6242d-119">Microsoft simge sunucuları altında listelendiğini doğrulayın **simge (.pdb) dosya konumları**.</span><span class="sxs-lookup"><span data-stu-id="6242d-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="6242d-120">Ayrıca ek simge dosyaları olabilir http://referencesource.microsoft.com/symbols başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6242d-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Sembol Seçenekleri][4]

<span data-ttu-id="6242d-122">İsterseniz, basitleştirebilir hello raporları sadece kendi kodumu ayarlayarak bu hello profil oluşturucu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6242d-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="6242d-123">Yalnızca My etkin kodla işlevi çağrı yığınları tamamen iç toolibraries çağırır ve .NET Framework hello hello raporlardan gizli basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6242d-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="6242d-124">Merhaba üzerinde **Araçları** menüsünde seçin **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="6242d-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="6242d-125">Merhaba genişletin **performans araçları** düğümünü ve **genel**.</span><span class="sxs-lookup"><span data-stu-id="6242d-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="6242d-126">Merhaba onay kutusunu seçip **sadece kendi kodumu etkinleştir profil oluşturucu raporlar için**.</span><span class="sxs-lookup"><span data-stu-id="6242d-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Yalnızca kendi kodum seçenekleri][17]

<span data-ttu-id="6242d-128">Bu yönergeler, var olan bir proje veya yeni bir proje ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="6242d-129">Aşağıda açıklanan teknikleri yeni bir proje tootry hello oluşturursanız, C# seçin **Azure bulut hizmeti** proje ve seçin bir **Web rolü** ve **çalışan rolü**.</span><span class="sxs-lookup"><span data-stu-id="6242d-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure bulut hizmeti projesi rolleri][5]

<span data-ttu-id="6242d-131">Örneğin, amaçları için çok zaman alır ve bazı bariz performans sorununu gösterir bazı kod tooyour projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6242d-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="6242d-132">Örneğin, kod tooa çalışan rolü projesi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6242d-132">For example, add hello following code tooa worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="6242d-133">Bu kod hello hello çalışan rolün RoleEntryPoint türetilmiş sınıf RunAsync yönteminde çağırmanıza.</span><span class="sxs-lookup"><span data-stu-id="6242d-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="6242d-134">(Zaman uyumlu olarak çalışan hello yöntemi hakkında hello uyarıyı yok sayın.)</span><span class="sxs-lookup"><span data-stu-id="6242d-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="6242d-135">Derleme ve bulut hizmetinizi yerel olarak (Ctrl + F5) hata ayıklama olmadan hello çözüm yapılandırma çok kümesi çalıştırma**sürüm**.</span><span class="sxs-lookup"><span data-stu-id="6242d-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="6242d-136">Bu, tüm dosya ve klasörlerin hello uygulama yerel olarak çalıştırmak için oluşturulur ve tüm hello Öykünücüler başlatıldığını sağlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="6242d-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="6242d-137">Merhaba işlem öykünücüsü kullanıcı Arabiriminde, çalışan rolü çalıştıran hello görev tooverify başlatın.</span><span class="sxs-lookup"><span data-stu-id="6242d-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="6242d-138">2: tooa işlem ekleme</span><span class="sxs-lookup"><span data-stu-id="6242d-138">2: Attach tooa process</span></span>
<span data-ttu-id="6242d-139">Visual Studio 2010 IDE hello başlatarak Merhaba uygulaması profil yerine, işlem çalışan hello profil oluşturucu tooa ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242d-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="6242d-140">tooattach hello profil oluşturucu tooa işlemi, hello **Çözümle** menüsünde seçin **profil oluşturucu** ve **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="6242d-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Profil seçeneği ekleme][6]

<span data-ttu-id="6242d-142">Çalışan rolü için hello WaWorkerHost.exe işlem bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6242d-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![WaWorkerHost işlemi][7]

<span data-ttu-id="6242d-144">Hello profil oluşturucu proje klasörünüzdeki bir ağ sürücüsündeyse, başka bir konum toosave hello profil oluşturma raporları tooprovide sorar.</span><span class="sxs-lookup"><span data-stu-id="6242d-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="6242d-145">Tooa web rolü tooWaIISHost.exe ekleyerek de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="6242d-146">Toouse hello ProcessId toodistinguish ihtiyacınız uygulamanızda birden çok rol işçi varsa, bunları.</span><span class="sxs-lookup"><span data-stu-id="6242d-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="6242d-147">Merhaba işlem nesnesi erişerek hello ProcessId program aracılığıyla sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="6242d-148">Örneğin, bir rolde bu kodu toohello Çalıştır yöntemi hello RoleEntryPoint türetilmiş sınıf eklerseniz, hello işlem öykünücüsü kullanıcı Arabiriminde tooknow hangi işlem tooconnect günlüğüne bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="6242d-149">tooview hello günlüğü, başlangıç hello işlem öykünücüsü kullanıcı Arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="6242d-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Merhaba işlem öykünücüsü kullanıcı arabirimini Başlat][8]

<span data-ttu-id="6242d-151">Merhaba çalışan rolü günlük konsol penceresinde hello konsol penceresinin başlık çubuğunda tıklayarak hello işlem öykünücüsü kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="6242d-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="6242d-152">Merhaba işlem kimliği hello günlüğünde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-152">You can see hello process ID in hello log.</span></span>

![Görünüm işlem kimliği][9]

<span data-ttu-id="6242d-154">Bir bağlı uygulamanızın (gerekirse) UI tooreproduce hello senaryoda hello adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6242d-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="6242d-155">Toostop profil istediğinizde hello seçin **durdurmak profil** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="6242d-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Seçeneği profil oluşturmayı durdurmak][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="6242d-157">3: performans raporları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="6242d-157">3: View performance reports</span></span>
<span data-ttu-id="6242d-158">Merhaba performans raporu, uygulamanız için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6242d-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="6242d-159">Bu noktada, hello profil oluşturucu yürütülürken durdurur, veri .vsp dosyası olarak kaydeder ve bu verilerin analizini gösteren bir rapor görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6242d-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Profil Oluşturucu raporu][11]

<span data-ttu-id="6242d-161">Hello String.wstrcpy görürseniz etkin yolunuzda, sadece kendi kodumu toochange hello tıklatıldığında yalnızca tooshow kullanıcı kodu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6242d-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="6242d-162">String.Concat görürseniz, hello Göster tüm kod düğmesine basarak deneyin.</span><span class="sxs-lookup"><span data-stu-id="6242d-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="6242d-163">Merhaba Birleştir yöntemi ve büyük bölümünü hello yürütme süresi alma String.Concat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242d-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Analiz raporu][12]

<span data-ttu-id="6242d-165">Bu makalede hello dize birleştirme kod eklediyseniz, bu uyarı hello görev listesi olarak görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6242d-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="6242d-166">Oluşturulan ve atıldı dizeleri toohello sayısı çöp toplama aşırı miktarda olduğunu belirten bir uyarı da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Performans uyarıları][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="6242d-168">4: değişiklikleri yapın ve performans karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="6242d-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="6242d-169">Merhaba performans önce ve sonra bir kod değişikliği de karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="6242d-170">İşlem çalışan hello durdurmak ve hello kodu tooreplace hello dize birleştirme işlemi hello kullanımıyla StringBuilder'ın düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="6242d-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="6242d-171">Başka bir performans çalışma yapın ve ardından hello performans karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="6242d-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="6242d-172">Hello performans Gezgini, hello çalıştırır hello demektir aynı oturum, yalnızca her iki raporu seçebilir, hello kısayol menüsünü açın ve seçin **karşılaştırmak performans raporları**.</span><span class="sxs-lookup"><span data-stu-id="6242d-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6242d-173">Başka bir performans oturumda çalıştırılan toocompare istiyorsanız hello açın **Çözümle** menüsünde ve **karşılaştırmak performans raporları**.</span><span class="sxs-lookup"><span data-stu-id="6242d-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6242d-174">Her iki dosya görüntülenen hello iletişim kutusunda belirtin.</span><span class="sxs-lookup"><span data-stu-id="6242d-174">Specify both files in hello dialog box that appears.</span></span>

![Performans raporları seçeneği Karşılaştır][15]

<span data-ttu-id="6242d-176">Merhaba raporları hello iki çalışması arasındaki farklar vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="6242d-176">hello reports highlight differences between hello two runs.</span></span>

![Karşılaştırma raporu][16]

<span data-ttu-id="6242d-178">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="6242d-178">Congratulations!</span></span> <span data-ttu-id="6242d-179">Hello Profil Oluşturucu ile başladıktan.</span><span class="sxs-lookup"><span data-stu-id="6242d-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6242d-180">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="6242d-180">Troubleshooting</span></span>
* <span data-ttu-id="6242d-181">Yayın derlemesi profil ve hata ayıklama olmadan Başlat emin olun.</span><span class="sxs-lookup"><span data-stu-id="6242d-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="6242d-182">Hello profil oluşturucu menüsünde Hello Attach/Detach seçeneği etkin değilse hello performans Sihirbazı'nı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6242d-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="6242d-183">Merhaba işlem öykünücüsü kullanıcı Arabiriminde tooview hello uygulamanızın durumunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6242d-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="6242d-184">Uygulamaları hello öykünücüsünde başlatma ile ilgili sorunlar varsa veya hello profil oluşturucu ekleme hello işlem öykünücüsü kapatın ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="6242d-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="6242d-185">Bu hello sorunu çözmezse, yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="6242d-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="6242d-186">Merhaba işlem öykünücüsü toosuspend kullanın ve çalışan dağıtımları kaldırırsanız bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="6242d-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="6242d-187">Komutları komut satırından profil oluşturma hello birini kullandıysanız, özellikle genel ayarları Merhaba, VSPerfClrEnv /globaloff çağrıldı ve VsPerfMon.exe kapatıldı emin olun.</span><span class="sxs-lookup"><span data-stu-id="6242d-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="6242d-188">Örnekleme yaparken hello iletiyi görürseniz "PRF0025: Toplanan hiçbir veriler," toohas CPU etkinlik bağlı işlem hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6242d-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="6242d-189">Herhangi bir hesaplama iş yapmamanın uygulamaları herhangi bir örnekleme veri oluşturamayabilir.</span><span class="sxs-lookup"><span data-stu-id="6242d-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="6242d-190">Tüm örnekleme yapıldığı önce hello işlem çıktı mümkündür.</span><span class="sxs-lookup"><span data-stu-id="6242d-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="6242d-191">Run yöntemi profil bir rol için hello onay toosee Sonlandır değil.</span><span class="sxs-lookup"><span data-stu-id="6242d-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6242d-192">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6242d-192">Next Steps</span></span>
<span data-ttu-id="6242d-193">Azure ikili hello öykünücüsü dosyalarda düzenleme hello Visual Studio profil oluşturucu içinde desteklenmez, ancak tootest bellek ayırma istiyorsanız, profil olduğunda bu seçeneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6242d-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="6242d-194">Ayrıca eşzamanlılık profili oluşturma, iş parçacığı için kilit zaman rekabet israfı olup olmadığını belirlemek ya da katman etkileşim profil, bir uygulama katmanları arasında kullanılırken performans sorunları izlemenize yardımcı olan en yardımcı olan seçebilirsiniz sık sık hello veri katmanı ve çalışan rolü arasında.</span><span class="sxs-lookup"><span data-stu-id="6242d-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="6242d-195">Uygulamanızı oluşturur hello veritabanı sorgularını görüntüleyin ve veri tooimprove hello veritabanı kullanımınız profil hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="6242d-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="6242d-196">Merhaba blog gönderisi katman etkileşim profil hakkında daha fazla bilgi için bkz [izlenecek yol: Visual Studio Team System 2010 katman etkileşim profil oluşturucu hello kullanarak][3].</span><span class="sxs-lookup"><span data-stu-id="6242d-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
