---
title: "Bir bulut hizmeti yerel olarak işlem öykünücüsü'nde profil oluşturma | Microsoft Docs"
services: cloud-services
description: "Visual Studio Profil Oluşturucu ile bulut Hizmetleri performans sorunları araştırmak"
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
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="b7d7b-103">Bir bulut Hizmeti performansını Visual Studio profil oluşturucu kullanılarak Azure işlem öykünücüsü yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="b7d7b-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="b7d7b-104">Çeşitli araçları ve teknikleri, bulut Hizmetleri performansını test etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="b7d7b-105">Azure için bulut hizmeti yayımladığınızda, Visual Studio profil oluşturma verileri toplamak ve ardından analiz olabilir açıklandığı gibi yerel olarak [bir Azure uygulama profili oluşturma][1].</span><span class="sxs-lookup"><span data-stu-id="b7d7b-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="b7d7b-106">Ayrıca Tanılama performans sayaçları, çeşitli izlemek için açıklandığı gibi kullanabileceğiniz [Azure'da performans sayaçlarını kullanarak][2].</span><span class="sxs-lookup"><span data-stu-id="b7d7b-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="b7d7b-107">Buluta dağıtmadan önce uygulamanızda yerel olarak işlem öykünücüsü profil isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="b7d7b-108">Bu makale, öykünücüde yer olarak uygulanabilen, profil oluşturma için CPU Örnekleme yöntemini kapsar.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="b7d7b-109">CPU örnekleme, profil oluşturma yöntemi çok zorlayıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="b7d7b-110">Belirlenen örnekleme aralığı sırasında profil oluşturucu çağrı yığınının bir anlık görüntüsünü alır.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="b7d7b-111">Veriler, bir süre boyunca toplanan ve bir raporda.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="b7d7b-112">Profil oluşturma yöntemi, burada bir pkı'ya yoğun uygulamasında CPU işlerin çoğunu yapılır belirtmek eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="b7d7b-113">Bu, uygulamanızın en uzun süre burada harcama "etkin yolunuzda" odak fırsatı verir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="b7d7b-114">1: profil oluşturma için Visual Studio'yu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b7d7b-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="b7d7b-115">İlk olarak, profil oluşturma zaman yararlı olabilecek birkaç Visual Studio yapılandırma seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="b7d7b-116">Profil oluşturma raporları anlamlı için uygulama ve ayrıca sistem kitaplıkları simgelerini simge (.pdb dosyaları) gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="b7d7b-117">Kullanılabilir simge sunucuları başvuru emin olmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="b7d7b-118">Bunu yapmak için **Araçları** Visual Studio'da menüsünü seçin **seçenekleri**, ardından **hata ayıklama**, ardından **simgeleri**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="b7d7b-119">Microsoft simge sunucuları altında listelendiğini doğrulayın **simge (.pdb) dosya konumları**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="b7d7b-120">Ayrıca ek simge dosyaları olabilir http://referencesource.microsoft.com/symbols başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Sembol Seçenekleri][4]

<span data-ttu-id="b7d7b-122">İsterseniz, sadece kendi kodumu ayarlayarak profil oluşturucu oluşturur raporları basitleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="b7d7b-123">Böylece çağrıları kitaplıkları ve .NET Framework tamamen iç raporlarını gizli yalnızca My etkin kodla işlevi çağrı yığınları basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="b7d7b-124">Üzerinde **Araçları** menüsünde seçin **seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="b7d7b-125">Ardından **performans araçları** düğümü seçin **genel**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="b7d7b-126">Onay kutusunu seçip **sadece kendi kodumu etkinleştir profil oluşturucu raporlar için**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Yalnızca kendi kodum seçenekleri][17]

<span data-ttu-id="b7d7b-128">Bu yönergeler, var olan bir proje veya yeni bir proje ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="b7d7b-129">Aşağıda açıklanan teknikleri denemek için yeni bir proje oluşturursanız, C# seçin **Azure bulut hizmeti** proje ve seçin bir **Web rolü** ve **çalışan rolü**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure bulut hizmeti projesi rolleri][5]

<span data-ttu-id="b7d7b-131">Örneğin amaçları ekleyin biraz kod projenize çok zaman alır ve bazı bariz performans sorununu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="b7d7b-132">Örneğin, bir çalışan rolü projesi için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b7d7b-132">For example, add the following code to a worker role project:</span></span>

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

<span data-ttu-id="b7d7b-133">Bu kod çalışan rolün RoleEntryPoint türetilmiş sınıf RunAsync yönteminde çağırmanıza.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="b7d7b-134">(Zaman uyumlu olarak çalışan yöntemi hakkında uyarıyı yok sayın.)</span><span class="sxs-lookup"><span data-stu-id="b7d7b-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="b7d7b-135">Derleme ve bulut hizmetinizi yerel olarak (Ctrl + F5) hata ayıklama olmadan kümesine çözüm yapılandırması ile çalıştırma **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="b7d7b-136">Bu, tüm dosya ve klasörlerin uygulama yerel olarak çalıştırmak için oluşturulur ve tüm Öykünücüler başlatıldığını sağlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="b7d7b-137">İşlem öykünücüsü kullanıcı Arabiriminde çalışan rolünüzün çalıştığını doğrulamak için görev çubuğundan başlatın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="b7d7b-138">2: bir işlem ekleme</span><span class="sxs-lookup"><span data-stu-id="b7d7b-138">2: Attach to a process</span></span>
<span data-ttu-id="b7d7b-139">Visual Studio 2010 IDE'den başlatarak uygulama profil yerine, bir çalışan işlemi için profil oluşturucu ekleme gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="b7d7b-140">Üzerinde bir işlemi için profil oluşturucu ekleme için **Çözümle** menüsünde seçin **profil oluşturucu** ve **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Profil seçeneği ekleme][6]

<span data-ttu-id="b7d7b-142">Çalışan rolü için WaWorkerHost.exe işlem bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![WaWorkerHost işlemi][7]

<span data-ttu-id="b7d7b-144">Proje klasörünüzdeki bir ağ sürücüsündeyse profil oluşturucu profil oluşturma raporları kaydetmek için başka bir konum sağlamak üzere istenir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="b7d7b-145">Bir web rolü için WaIISHost.exe ekleyerek de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="b7d7b-146">Uygulamanızda birden çok rol işçi varsa, ProcessId bunları ayırt etmek için kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="b7d7b-147">İşlem nesnesi erişerek ProcessId program aracılığıyla sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="b7d7b-148">Örneğin, bir roldeki RoleEntryPoint türetilmiş sınıf Run yöntemi için bu kodu eklerseniz, bağlanmak için hangi işlemin bilmeniz işlem öykünücüsü UI günlüğüne bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="b7d7b-149">Günlüğünü görüntülemek için işlem öykünücüsü kullanıcı arabirimini Başlat.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-149">To view the log, start the Compute Emulator UI.</span></span>

![İşlem öykünücüsü kullanıcı arabirimini Başlat][8]

<span data-ttu-id="b7d7b-151">Çalışan rolü günlük konsol penceresi işlem öykünücüsü kullanıcı Arabiriminde, konsol penceresinin başlık çubuğunda tıklatarak açın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="b7d7b-152">İşlem kimliği günlüğünde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-152">You can see the process ID in the log.</span></span>

![Görünüm işlem kimliği][9]

<span data-ttu-id="b7d7b-154">Bir bağlı adımları gerçekleştirir, uygulamanın kullanıcı Arabiriminde (gerekirse) senaryoyu yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="b7d7b-155">Profil oluşturmayı durdurmak istediğinizde, belirleyin **durdurmak profil** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Seçeneği profil oluşturmayı durdurmak][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="b7d7b-157">3: performans raporları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="b7d7b-157">3: View performance reports</span></span>
<span data-ttu-id="b7d7b-158">Uygulamanız için performans raporu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="b7d7b-159">Bu noktada, profil oluşturucu yürütülürken durdurur, veri .vsp dosyası olarak kaydeder ve bu verilerin analizini gösteren bir rapor görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Profil Oluşturucu raporu][11]

<span data-ttu-id="b7d7b-161">Sık kullanılan yolundaki String.wstrcpy görürseniz, sadece kendi kullanıcı kodu yalnızca göstermek için görünümü değiştirmek için kodumu üzerinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="b7d7b-162">String.Concat görürseniz, tüm kod Göster düğmesine basarak deneyin.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="b7d7b-163">Birleştir yöntemi ve yürütme süresi büyük bir kısmı alma String.Concat görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Analiz raporu][12]

<span data-ttu-id="b7d7b-165">Bu makalede dize birleştirme kod eklediyseniz, bunun için bir uyarı görev listesinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="b7d7b-166">Oluşturulan ve atıldı dizeleri sayısı nedeniyle çöp toplama aşırı miktarda olduğunu belirten bir uyarı da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Performans uyarıları][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="b7d7b-168">4: değişiklikleri yapın ve performans karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="b7d7b-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="b7d7b-169">Önce ve sonra bir kod değişikliği performans de karşılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="b7d7b-170">Çalışan işlemi durdurmak ve dize birleştirme işlemi StringBuilder kullanımı ile değiştirmek için kod düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="b7d7b-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

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

<span data-ttu-id="b7d7b-171">Başka bir performans çalışma yapın ve ardından performans karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="b7d7b-172">Performans Explorer'ın çalıştığı aynı oturumda varsa, yalnızca her iki raporu seçebilir, kısayol menüsünü açın ve seçin **karşılaştırmak performans raporları**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="b7d7b-173">Başka bir performans oturumda çalıştırılan karşılaştırma yapmak isterseniz, açmak **Çözümle** menüsünde ve **karşılaştırmak performans raporları**.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="b7d7b-174">Görüntülenen iletişim kutusunda her iki dosya belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-174">Specify both files in the dialog box that appears.</span></span>

![Performans raporları seçeneği Karşılaştır][15]

<span data-ttu-id="b7d7b-176">Raporları iki çalışması arasındaki farklar vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-176">The reports highlight differences between the two runs.</span></span>

![Karşılaştırma raporu][16]

<span data-ttu-id="b7d7b-178">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="b7d7b-178">Congratulations!</span></span> <span data-ttu-id="b7d7b-179">Profil Oluşturucu ile başladıktan.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b7d7b-180">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b7d7b-180">Troubleshooting</span></span>
* <span data-ttu-id="b7d7b-181">Yayın derlemesi profil ve hata ayıklama olmadan Başlat emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="b7d7b-182">Profil Oluşturucu menüsünde Attach/Detach seçeneği etkin değilse, performans Sihirbazı'nı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="b7d7b-183">Uygulamanızın durumunu görüntülemek için işlem öykünücüsü kullanıcı arabirimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="b7d7b-184">Öykünücüde uygulamaları başlatma ile ilgili sorunlar varsa veya profil oluşturucu ekleme Kapat işlem öykünücüsü aşağı ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="b7d7b-185">Bu sorunu çözmezse, yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="b7d7b-186">Askıya alma ve çalışan dağıtımları kaldırmak için işlem öykünücüsü kullanıyorsanız bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="b7d7b-187">Özellikle genel ayarları, komut satırından profil oluşturma komutlardan herhangi birini kullandıysanız, VSPerfClrEnv /globaloff çağrıldı ve VsPerfMon.exe kapatıldı emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="b7d7b-188">Örnekleme yaparken iletisini görürseniz, "PRF0025: Toplanan hiçbir veriler,", ekli işlem CPU etkinliği olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="b7d7b-189">Herhangi bir hesaplama iş yapmamanın uygulamaları herhangi bir örnekleme veri oluşturamayabilir.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="b7d7b-190">Tüm örnekleme yapıldığı önce işlem çıktı mümkündür.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="b7d7b-191">Run yöntemi profil bir rol için değil sonlandırmak denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7d7b-192">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b7d7b-192">Next Steps</span></span>
<span data-ttu-id="b7d7b-193">Azure ikili öykünücü dosyalarda düzenleme Visual Studio Profil Oluşturucusu'nda desteklenmez, ancak bellek ayırma test etmek isterseniz, profil olduğunda bu seçeneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="b7d7b-194">Ayrıca eşzamanlılık profili oluşturma, iş parçacıkları performans sorunlarının en sık veri katmanı ve çalışan rolü arasındaki bir uygulama katmanları arasında kullanılırken izlemenize yardımcı olan kilitleri veya katman etkileşim profil, rekabet zaman olup olmadığını belirlemenize yardımcı olan tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="b7d7b-195">Uygulamanızı oluşturur veritabanı sorgularını görüntüleyin ve veritabanı kullanımınızı iyileştirmek için profil oluşturma verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7d7b-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="b7d7b-196">Katman etkileşimli profil oluşturma hakkında daha fazla bilgi için blog gönderisine bakın [izlenecek yol: Visual Studio Team System 2010'katman etkileşim Profiler kullanarak][3].</span><span class="sxs-lookup"><span data-stu-id="b7d7b-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
