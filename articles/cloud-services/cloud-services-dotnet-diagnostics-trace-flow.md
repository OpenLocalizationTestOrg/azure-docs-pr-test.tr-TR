---
title: "Bulut Hizmetleri uygulamasıyla Azure tanılama aaaTrace hello akışı | Microsoft Docs"
description: "İzleme iletileri tooan Azure uygulamanızı toohelp hata ayıklama, performansını ölçmek, izleme, trafik analizi ve daha ekleyin."
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
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="4aa7a-103">Bulut Hizmetleri uygulaması Azure Tanılama ile Merhaba akışını izleme</span><span class="sxs-lookup"><span data-stu-id="4aa7a-103">Trace hello flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="4aa7a-104">Çalışırken izleme, toomonitor hello yürütülmesi için uygulamanızın yoludur.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-104">Tracing is a way for you toomonitor hello execution of your application while it is running.</span></span> <span data-ttu-id="4aa7a-105">Merhaba kullanabilirsiniz [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), ve [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) sınıfları toorecord hatalar hakkında bilgi ve Uygulama yürütme günlükleri, metin dosyaları veya diğer cihazları daha sonra çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-105">You can use hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes toorecord information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="4aa7a-106">İzleme hakkında daha fazla bilgi için bkz: [izleme ve düzenleme uygulamaları](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="4aa7a-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="4aa7a-107">İzleme deyimleri ve izleme anahtarları kullanın</span><span class="sxs-lookup"><span data-stu-id="4aa7a-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="4aa7a-108">Uygulama izleme hello ekleyerek, bulut Hizmetleri uygulamanızda [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello uygulama yapılandırması ve yapma çağırır tooSystem.Diagnostics.Trace veya System.Diagnostics.Debug içinde uygulama kodu.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-108">Implement tracing in your Cloud Services application by adding hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello application configuration and making calls tooSystem.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="4aa7a-109">Kullanım hello yapılandırma dosyası *app.config* çalışan roller ve hello *web.config* web rolleri için.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-109">Use hello configuration file *app.config* for worker roles and hello *web.config* for web roles.</span></span> <span data-ttu-id="4aa7a-110">Visual Studio şablon kullanarak yeni bir barındırılan hizmet oluşturduğunuzda, Azure tanılama toohello proje otomatik olarak eklenir ve hello DiagnosticMonitorTraceListener toohello eklediğiniz hello rolleri için uygun yapılandırma dosyası eklenir.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added toohello project and hello DiagnosticMonitorTraceListener is added toohello appropriate configuration file for hello roles that you add.</span></span>

<span data-ttu-id="4aa7a-111">İzleme deyimleri yerleştirme hakkında daha fazla bilgi için bkz: [nasıl yapılır: izleme deyimleri ekleme tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4aa7a-111">For information on placing trace statements, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="4aa7a-112">Yerleştirerek [izleme anahtarları](https://msdn.microsoft.com/library/3at424ac.aspx) kodunuzda izleme olup oluşur ve ne kadar kapsamlı olduğunu denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="4aa7a-113">Uygulamanızı bir üretim ortamında hello durumunu izlemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-113">This lets you monitor hello status of your application in a production environment.</span></span> <span data-ttu-id="4aa7a-114">Birden çok bilgisayar üzerinde çalışan birden çok bileşenleri kullanan bir iş uygulaması bu durum özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="4aa7a-115">Daha fazla bilgi için bkz: [nasıl yapılır: izleme anahtarları yapılandırma](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="4aa7a-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-hello-trace-listener-in-an-azure-application"></a><span data-ttu-id="4aa7a-116">Bir Azure uygulamasında Hello İzleme dinleyicisi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4aa7a-116">Configure hello trace listener in an Azure application</span></span>
<span data-ttu-id="4aa7a-117">İzleme, hata ayıklama ve TraceSource, "dinleyicileri" toocollect ve gönderilen kayıt Merhaba iletileri ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-117">Trace, Debug and TraceSource, require you set up "listeners" toocollect and record hello messages that are sent.</span></span> <span data-ttu-id="4aa7a-118">Dinleyicileri toplamak, depolamak ve izleme iletileri yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="4aa7a-119">Bunlar hello İzleme çıktısı tooan uygun hedef, günlük, pencere veya metin dosyası gibi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-119">They direct hello tracing output tooan appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="4aa7a-120">Azure tanılama kullanan hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-120">Azure Diagnostics uses hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="4aa7a-121">Aşağıdaki yordamı hello tamamlamadan önce hello Azure Tanılama izleme başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-121">Before you complete hello following procedure, you must initialize hello Azure diagnostic monitor.</span></span> <span data-ttu-id="4aa7a-122">toodo Bu, bkz: [Microsoft Azure tanılama etkinleştirme](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="4aa7a-122">toodo this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="4aa7a-123">Visual Studio tarafından sağlanan hello şablonları kullanırsanız, hello dinleyicisi hello yapılandırmasını otomatik olarak sizin yerinize eklendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-123">Note that if you use hello templates that are provided by Visual Studio, hello configuration of hello listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="4aa7a-124">İzleme dinleyicisi ekleme</span><span class="sxs-lookup"><span data-stu-id="4aa7a-124">Add a trace listener</span></span>
1. <span data-ttu-id="4aa7a-125">Rolünüz için Hello web.config veya app.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-125">Open hello web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="4aa7a-126">Aşağıdaki kod toohello dosyasına hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-126">Add hello following code toohello file.</span></span> <span data-ttu-id="4aa7a-127">Başvurduğunuz hello derlemenin Hello sürüm özniteliği toouse hello sürüm numarasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-127">Change hello Version attribute toouse hello version number of hello assembly you are referencing.</span></span> <span data-ttu-id="4aa7a-128">güncelleştirmeleri tooit olmadıkça hello derleme sürümü her Azure SDK sürümüyle mutlaka değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-128">hello assembly version does not necessarily change with each Azure SDK release unless there are updates tooit.</span></span>
   
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
   > <span data-ttu-id="4aa7a-129">Bir proje başvurusu toohello Microsoft.WindowsAzure.Diagnostics derleme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-129">Make sure you have a project reference toohello Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="4aa7a-130">Güncelleştirme hello sürüm numarası hello XML toomatch hello hello sürümü yukarıda Microsoft.WindowsAzure.Diagnostics derleme başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-130">Update hello version number in hello xml above toomatch hello version of hello referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="4aa7a-131">Merhaba yapılandırma dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-131">Save hello config file.</span></span>

<span data-ttu-id="4aa7a-132">Dinleyicileri hakkında daha fazla bilgi için bkz: [izleme dinleyicileri](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="4aa7a-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="4aa7a-133">Merhaba adımları tooadd hello dinleyicisi tamamladıktan sonra izleme deyimleri tooyour kodu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-133">After you complete hello steps tooadd hello listener, you can add trace statements tooyour code.</span></span>

### <a name="tooadd-trace-statement-tooyour-code"></a><span data-ttu-id="4aa7a-134">tooadd izleme deyimi tooyour kodu</span><span class="sxs-lookup"><span data-stu-id="4aa7a-134">tooadd trace statement tooyour code</span></span>
1. <span data-ttu-id="4aa7a-135">Uygulamanız için bir kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-135">Open a source file for your application.</span></span> <span data-ttu-id="4aa7a-136">Örneğin, hello <RoleName>.cs dosyası hello çalışan rolü veya web rolü.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-136">For example, hello <RoleName>.cs file for hello worker role or web role.</span></span>
2. <span data-ttu-id="4aa7a-137">Merhaba aşağıdakileri ekleyin zaten eklenemiyor deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="4aa7a-137">Add hello following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="4aa7a-138">Uygulamanızı hello durumu hakkında toocapture bilgi istediğiniz yere izleme deyimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-138">Add Trace statements where you want toocapture information about hello state of your application.</span></span> <span data-ttu-id="4aa7a-139">Yöntemleri tooformat hello hello izleme deyimi çıktısını çeşitli kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-139">You can use a variety of methods tooformat hello output of hello Trace statement.</span></span> <span data-ttu-id="4aa7a-140">Daha fazla bilgi için bkz: [nasıl yapılır: izleme deyimleri ekleme tooApplication kod](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="4aa7a-140">For more information, see [How to: Add Trace Statements tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="4aa7a-141">Merhaba kaynak dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4aa7a-141">Save hello source file.</span></span>

