---
title: "Bulut Hizmetleri uygulamasıyla Azure tanılama akışında izleme | Microsoft Docs"
description: "İzleme iletileri hata ayıklama, performans, izleme, trafik analizi ve daha fazla ölçme yardımcı olmak için bir Azure uygulamaya ekleyin."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="a49eb-103">Bulut Hizmetleri uygulaması Azure Tanılama ile akışı izleme</span><span class="sxs-lookup"><span data-stu-id="a49eb-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="a49eb-104">İzleme, çalışırken, uygulamanızın yürütülmesini izlemek bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="a49eb-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="a49eb-105">Kullanabileceğiniz [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), ve [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) hatalarla ilgili bilgileri kaydetmek için sınıflar ve Uygulama yürütme günlükleri, metin dosyaları veya diğer cihazları daha sonra çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="a49eb-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="a49eb-106">İzleme hakkında daha fazla bilgi için bkz: [izleme ve düzenleme uygulamaları](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49eb-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="a49eb-107">İzleme deyimleri ve izleme anahtarları kullanın</span><span class="sxs-lookup"><span data-stu-id="a49eb-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="a49eb-108">Uygulama izleme ekleyerek, bulut Hizmetleri uygulamanızda [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) uygulama yapılandırmasını ve System.Diagnostics.Trace veya System.Diagnostics.Debug içinde çağrıları yapma, uygulama kodu.</span><span class="sxs-lookup"><span data-stu-id="a49eb-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="a49eb-109">Yapılandırma dosyası kullanın *app.config* çalışan rolleri için ve *web.config* web rolleri için.</span><span class="sxs-lookup"><span data-stu-id="a49eb-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="a49eb-110">Visual Studio şablon kullanarak yeni bir barındırılan hizmet oluşturduğunuzda, Azure tanılama projenize otomatik olarak eklenir ve DiagnosticMonitorTraceListener eklediğiniz rolleri için uygun yapılandırma dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="a49eb-111">İzleme deyimleri yerleştirme hakkında daha fazla bilgi için bkz: [nasıl yapılır: uygulama koduna izleme deyimleri ekleme](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49eb-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="a49eb-112">Yerleştirerek [izleme anahtarları](https://msdn.microsoft.com/library/3at424ac.aspx) kodunuzda izleme olup oluşur ve ne kadar kapsamlı olduğunu denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a49eb-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="a49eb-113">Uygulamanızı bir üretim ortamında durumunu izlemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="a49eb-114">Birden çok bilgisayar üzerinde çalışan birden çok bileşenleri kullanan bir iş uygulaması bu durum özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="a49eb-115">Daha fazla bilgi için bkz: [nasıl yapılır: izleme anahtarları yapılandırma](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49eb-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="a49eb-116">Bir Azure uygulamasında İzleme dinleyicisi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a49eb-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="a49eb-117">İzleme, hata ayıklama ve TraceSource, "toplamak ve gönderilen iletileri kaydetmek için dinleyicileri" ayarlamanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="a49eb-118">Dinleyicileri toplamak, depolamak ve izleme iletileri yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="a49eb-119">Bunlar, izleme çıktısı günlüğü, pencere veya metin dosyası gibi uygun bir hedefe yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="a49eb-120">Azure tanılama kullanan [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="a49eb-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="a49eb-121">Aşağıdaki yordamı tamamlamadan önce Azure Tanılama izleme başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a49eb-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="a49eb-122">Bunu yapmak için bkz: [Microsoft Azure tanılama etkinleştirme](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a49eb-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="a49eb-123">Visual Studio tarafından sağlanan şablonları kullanırsanız, dinleyiciyi yapılandırmasını otomatik olarak sizin yerinize eklendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="a49eb-124">İzleme dinleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="a49eb-124">Add a trace listener</span></span>
1. <span data-ttu-id="a49eb-125">Rolünüz için web.config veya app.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a49eb-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="a49eb-126">Dosyasına aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-126">Add the following code to the file.</span></span> <span data-ttu-id="a49eb-127">Version özniteliği başvurduğunuz derlemenin sürüm numarasını kullanmak üzere değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="a49eb-128">Güncelleştirmeleri olmadıkça derleme sürümünü her Azure SDK sürümüyle mutlaka değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="a49eb-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="a49eb-129">Proje başvurusu Microsoft.WindowsAzure.Diagnostics derleme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a49eb-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="a49eb-130">Başvurulan Microsoft.WindowsAzure.Diagnostics derleme sürümüyle eşleşecek şekilde yukarıdaki xml sürüm numarasını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="a49eb-131">Yapılandırma dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-131">Save the config file.</span></span>

<span data-ttu-id="a49eb-132">Dinleyicileri hakkında daha fazla bilgi için bkz: [izleme dinleyicileri](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49eb-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="a49eb-133">Dinleyici ekleme adımları tamamladıktan sonra kodunuzu izleme deyimleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a49eb-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="a49eb-134">Kodunuzda izleme deyimi eklemek için</span><span class="sxs-lookup"><span data-stu-id="a49eb-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="a49eb-135">Uygulamanız için bir kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a49eb-135">Open a source file for your application.</span></span> <span data-ttu-id="a49eb-136">Örneğin, <RoleName>web rolü ve çalışan rolü için .cs dosyası.</span><span class="sxs-lookup"><span data-stu-id="a49eb-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="a49eb-137">Aşağıdakileri ekleyin zaten eklenemiyor deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="a49eb-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="a49eb-138">Uygulamanızı durumuyla ilgili bilgileri yakalamak istediğiniz izleme deyimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="a49eb-139">İzleme deyimi çıktısını biçimlendirmek için çeşitli yöntemler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a49eb-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="a49eb-140">Daha fazla bilgi için bkz: [nasıl yapılır: uygulama koduna izleme deyimleri ekleme](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="a49eb-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="a49eb-141">Kaynak dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a49eb-141">Save the source file.</span></span>

