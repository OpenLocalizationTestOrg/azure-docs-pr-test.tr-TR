---
title: "Azure bulut hizmetlerine başlangıç görevleri çalıştırmak | Microsoft Docs"
description: "Başlangıç görevi, bulut hizmeti ortamınızı uygulamanız için hazırlanmanıza yardımcı. Bu, başlangıç görevleri nasıl çalıştığını ve bunları nasıl öğretir"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 1c1b3aa86dc8211de0c07c9fb68da5685c86f551
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="f410e-104">Nasıl yapılandırılacağı ve bir bulut hizmeti için başlangıç görevleri Çalıştır</span><span class="sxs-lookup"><span data-stu-id="f410e-104">How to configure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="f410e-105">Başlangıç görevi, bir rol başlamadan önce işlemlerini gerçekleştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f410e-105">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="f410e-106">Bir bileşeni yüklemek, COM bileşenlerini kaydetme, kayıt defteri anahtarlarını ayarlamak veya uzun süre çalışan bir işlem başlatılıyor gerçekleştirmek isteyebileceğiniz işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f410e-106">Operations that you might want to perform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="f410e-107">Başlangıç görevi sanal makineler için yalnızca bulut hizmeti Web ve çalışan rolleri için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="f410e-107">Startup tasks are not applicable to Virtual Machines, only to Cloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="f410e-108">Başlangıç görevi nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="f410e-108">How startup tasks work</span></span>
<span data-ttu-id="f410e-109">Başlangıç görevlerdir rollerinizi başlar ve içinde tanımlanan önce gerçekleştirilen eylemler [ServiceDefinition.csdef] kullanarak dosya [görev] öğesi içinde [başlangıç] öğesi.</span><span class="sxs-lookup"><span data-stu-id="f410e-109">Startup tasks are actions that are taken before your roles begin and are defined in the [ServiceDefinition.csdef] file by using the [Task] element within the [Startup] element.</span></span> <span data-ttu-id="f410e-110">Sık başlangıç görevleri toplu dosyalar, ancak bunlar aynı zamanda konsol uygulamaları veya PowerShell komut dosyalarını Başlat toplu iş dosyaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="f410e-111">Ortam değişkenleri, bir başlangıç görevi bilgi aktarmak ve yerel depolama bir başlangıç görevi dışında bilgi geçirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-111">Environment variables pass information into a startup task, and local storage can be used to pass information out of a startup task.</span></span> <span data-ttu-id="f410e-112">Örneğin, bir ortam değişkeni yüklemek istediğiniz program yolu belirtebilirsiniz ve ardından daha sonra rolleri tarafından okunabilir yerel depolama alanına dosyalar yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-112">For example, an environment variable can specify the path to a program you want to install, and files can be written to local storage that can then be read later by your roles.</span></span>

<span data-ttu-id="f410e-113">Başlangıç görevi bilgileri ve hataları tarafından belirtilen dizin oturum **TEMP** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f410e-113">Your startup task can log information and errors to the directory specified by the **TEMP** environment variable.</span></span> <span data-ttu-id="f410e-114">Başlangıç görevi sırasında **TEMP** ortam değişkenini çözümler için *C:\\kaynakları\\temp\\[GUID]. [ Rol adı]\\RoleTemp* bulut üzerinde çalışırken dizin.</span><span class="sxs-lookup"><span data-stu-id="f410e-114">During the startup task, the **TEMP** environment variable resolves to the *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on the cloud.</span></span>

<span data-ttu-id="f410e-115">Başlangıç görevi yeniden başlatmalar arasında da birkaç kez çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="f410e-116">Örneğin, başlangıç görevi rol geri dönüştürme her zaman çalıştırılır ve rol dönüştürür her zaman yeniden başlatma içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-116">For example, the startup task will be run each time the role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="f410e-117">Başlangıç görevi, bunları birkaç kez sorunsuz çalışmasına izin veren şekilde yazılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f410e-117">Startup tasks should be written in a way that allows them to run several times without problems.</span></span>

<span data-ttu-id="f410e-118">Başlangıç görevleri ile bitmelidir bir **errorlevel** (veya çıkış kodu) başlatma işlemini tamamlamak için sıfır.</span><span class="sxs-lookup"><span data-stu-id="f410e-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for the startup process to complete.</span></span> <span data-ttu-id="f410e-119">Bir başlangıç görevi bir sıfır ile bitip bitmediğini **errorlevel**, rol başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="f410e-119">If a startup task ends with a non-zero **errorlevel**, the role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="f410e-120">Rol başlatma sırası</span><span class="sxs-lookup"><span data-stu-id="f410e-120">Role startup order</span></span>
<span data-ttu-id="f410e-121">Azure rol başlangıç yordamda listeler:</span><span class="sxs-lookup"><span data-stu-id="f410e-121">The following lists the role startup procedure in Azure:</span></span>

1. <span data-ttu-id="f410e-122">Örnek olarak işaretlenmiş **başlangıç** ve trafik almaz.</span><span class="sxs-lookup"><span data-stu-id="f410e-122">The instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="f410e-123">Tüm başlangıç görevleri göre yürütülür kendi **taskType** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f410e-123">All startup tasks are executed according to their **taskType** attribute.</span></span>
   
   * <span data-ttu-id="f410e-124">**Basit** görevler eşzamanlı olarak, yürütülen bir kerede.</span><span class="sxs-lookup"><span data-stu-id="f410e-124">The **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="f410e-125">**Arka plan** ve **ön plan** görevleri başlangıç görevi başlatılacağı zaman uyumsuz olarak, paralel.</span><span class="sxs-lookup"><span data-stu-id="f410e-125">The **background** and **foreground** tasks are started asynchronously, parallel to the startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="f410e-126">Role özgü verileri kullanılabilir olmaması IIS tam olarak başlatma işleminde, başlangıç görevi aşaması sırasında yapılandırılmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-126">IIS may not be fully configured during the startup task stage in the startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="f410e-127">Role özgü veri gerektiren başlangıç görevleri kullanması gereken [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="f410e-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="f410e-128">Rol ana bilgisayar işlemi başlatıldı ve sitesi IIS içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f410e-128">The role host process is started and the site is created in IIS.</span></span>
4. <span data-ttu-id="f410e-129">[Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="f410e-129">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="f410e-130">Örnek olarak işaretlenmiş **hazır** ve trafik örneğine yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-130">The instance is marked as **Ready** and traffic is routed to the instance.</span></span>
6. <span data-ttu-id="f410e-131">[Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="f410e-131">The [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="f410e-132">Bir başlangıç görevi örneği</span><span class="sxs-lookup"><span data-stu-id="f410e-132">Example of a startup task</span></span>
<span data-ttu-id="f410e-133">Başlangıç görevi tanımlanmış [ServiceDefinition.csdef] dosyasında **görev** öğesi.</span><span class="sxs-lookup"><span data-stu-id="f410e-133">Startup tasks are defined in the [ServiceDefinition.csdef] file, in the **Task** element.</span></span> <span data-ttu-id="f410e-134">**CommandLine** özniteliği, adını ve başlangıç toplu iş dosyasını veya konsol komutunu, parametrelerini belirtir **executionContext** özniteliği başlangıç görevinin ayrıcalık düzeyi belirtir ve **taskType** özniteliği, görevin nasıl yürütülecek belirtir.</span><span class="sxs-lookup"><span data-stu-id="f410e-134">The **commandLine** attribute specifies the name and parameters of the startup batch file or console command, the **executionContext** attribute specifies the privilege level of the startup task, and the **taskType** attribute specifies how the task will be executed.</span></span>

<span data-ttu-id="f410e-135">Bu örnekte, bir ortam değişkeni **MyVersionNumber**, başlangıç görevi oluşturulur ve değerine ayarlayın "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="f410e-135">In this example, an environment variable, **MyVersionNumber**, is created for the startup task and set to the value "**1.0.0.0**".</span></span>

<span data-ttu-id="f410e-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="f410e-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="f410e-137">Aşağıdaki örnekte, **Startup.cmd** toplu iş dosyası "geçerli sürüm 1.0.0.0 StartupLog.txt dosyasına TEMP ortam değişkeni tarafından belirtilen dizinde." satır yazar.</span><span class="sxs-lookup"><span data-stu-id="f410e-137">In the following example, the **Startup.cmd** batch file writes the line "The current version is 1.0.0.0" to the StartupLog.txt file in the directory specified by the TEMP environment variable.</span></span> <span data-ttu-id="f410e-138">`EXIT /B 0` Satır sağlar başlangıç görevi ile biten bir **errorlevel** sıfır.</span><span class="sxs-lookup"><span data-stu-id="f410e-138">The `EXIT /B 0` line ensures that the startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO The current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="f410e-139">Visual Studio'da **çıktı dizinine Kopyala** özelliği başlangıç toplu işlem dosyanız için ayarlanmalıdır **her zaman Kopyala** başlangıç toplu iş dosyası projenize Azure üzerinde düzgün bir şekilde dağıtıldıktan emin olmak için (**approot\\bin** Web rolleri için ve **approot** çalışan roller için).</span><span class="sxs-lookup"><span data-stu-id="f410e-139">In Visual Studio, the **Copy to Output Directory** property for your startup batch file should be set to **Copy Always** to be sure that your startup batch file is properly deployed to your project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="f410e-140">Görev öznitelikler açıklaması</span><span class="sxs-lookup"><span data-stu-id="f410e-140">Description of task attributes</span></span>
<span data-ttu-id="f410e-141">Aşağıdaki özniteliklerini açıklayan **görev** öğesinde [ServiceDefinition.csdef] dosyası:</span><span class="sxs-lookup"><span data-stu-id="f410e-141">The following describes the attributes of the **Task** element in the [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="f410e-142">**komut satırı** -başlangıç görevinin komut satırını belirtir:</span><span class="sxs-lookup"><span data-stu-id="f410e-142">**commandLine** - Specifies the command line for the startup task:</span></span>

* <span data-ttu-id="f410e-143">Başlangıç görevi başlatan komutuyla, isteğe bağlı komut satırı parametreleri.</span><span class="sxs-lookup"><span data-stu-id="f410e-143">The command, with optional command line parameters, which begins the startup task.</span></span>
* <span data-ttu-id="f410e-144">Sık .cmd veya .bat toplu dosyanın budur.</span><span class="sxs-lookup"><span data-stu-id="f410e-144">Frequently this is the filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="f410e-145">AppRoot göre görevdir\\Bin klasörü dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="f410e-145">The task is relative to the AppRoot\\Bin folder for the deployment.</span></span> <span data-ttu-id="f410e-146">Ortam değişkenleri yolu ve dosya görevinin belirlerken genişletilir değil.</span><span class="sxs-lookup"><span data-stu-id="f410e-146">Environment variables are not expanded in determining the path and file of the task.</span></span> <span data-ttu-id="f410e-147">Ortam genişletme gerekiyorsa, başlangıç görevi çağıran bir küçük .cmd komut dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f410e-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="f410e-148">Bir konsol uygulaması ya da başlayan bir toplu iş dosyası bir [PowerShell Betiği](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="f410e-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="f410e-149">**executionContext** -başlangıç görevi ayrıcalık düzeyini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f410e-149">**executionContext** - Specifies the privilege level for the startup task.</span></span> <span data-ttu-id="f410e-150">Ayrıcalık düzeyi sınırlı veya yükseltilmiş:</span><span class="sxs-lookup"><span data-stu-id="f410e-150">The privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="f410e-151">**sınırlı**</span><span class="sxs-lookup"><span data-stu-id="f410e-151">**limited**</span></span>  
  <span data-ttu-id="f410e-152">Başlangıç görevi rolle aynı ayrıcalıklarıyla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f410e-152">The startup task runs with the same privileges as the role.</span></span> <span data-ttu-id="f410e-153">Zaman **executionContext** için öznitelik [çalışma zamanı] öğesidir de **sınırlı**, kullanıcı ayrıcalıkları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f410e-153">When the **executionContext** attribute for the [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="f410e-154">**yükseltilmiş**</span><span class="sxs-lookup"><span data-stu-id="f410e-154">**elevated**</span></span>  
  <span data-ttu-id="f410e-155">Başlangıç görevi yönetici ayrıcalıklarıyla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f410e-155">The startup task runs with administrator privileges.</span></span> <span data-ttu-id="f410e-156">Bu programları yükleyin, IIS yapılandırma değişiklikleri, kayıt defteri değişiklikleri gerçekleştirmek için başlangıç görevleri ve diğer yönetici düzeyi görevleri rol ayrıcalık düzeyi artırmadan sağlar.</span><span class="sxs-lookup"><span data-stu-id="f410e-156">This allows startup tasks to install programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing the privilege level of the role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="f410e-157">Bir başlangıç görevi ayrıcalık düzeyi rolü ile aynı olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f410e-157">The privilege level of a startup task does not need to be the same as the role itself.</span></span>
> 
> 

<span data-ttu-id="f410e-158">**taskType** -başlangıç görevi yürütüldüğünde yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="f410e-158">**taskType** - Specifies the way a startup task is executed.</span></span>

* <span data-ttu-id="f410e-159">**Basit**</span><span class="sxs-lookup"><span data-stu-id="f410e-159">**simple**</span></span>  
  <span data-ttu-id="f410e-160">Görevler eşzamanlı olarak, yürütülen bir kerede, belirtilen sırada [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="f410e-160">Tasks are executed synchronously, one at a time, in the order specified in the [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="f410e-161">Bir zaman **basit** başlangıç görevi sonlandırır ile bir **errorlevel** sıfır, sonraki **basit** başlangıç görevi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f410e-161">When one **simple** startup task ends with an **errorlevel** of zero, the next **simple** startup task is executed.</span></span> <span data-ttu-id="f410e-162">Artık böyle olduğunda **basit** rol kendisi başlatılır sonra yürütülecek başlangıç görevi.</span><span class="sxs-lookup"><span data-stu-id="f410e-162">If there are no more **simple** startup tasks to execute, then the role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="f410e-163">Varsa **basit** görev bir sıfır ile biten **errorlevel**, örnek engellenir.</span><span class="sxs-lookup"><span data-stu-id="f410e-163">If the **simple** task ends with a non-zero **errorlevel**, the instance will be blocked.</span></span> <span data-ttu-id="f410e-164">Sonraki **basit** başlangıç görevleri ve rol kendisinin başlatılmayacak.</span><span class="sxs-lookup"><span data-stu-id="f410e-164">Subsequent **simple** startup tasks, and the role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="f410e-165">Toplu iş dosyası ile biten emin olmak için bir **errorlevel** hiç biri komutu yürütün `EXIT /B 0` toplu iş dosyası işleminin sonunda.</span><span class="sxs-lookup"><span data-stu-id="f410e-165">To ensure that your batch file ends with an **errorlevel** of zero, execute the command `EXIT /B 0` at the end of your batch file process.</span></span>
* <span data-ttu-id="f410e-166">**arka plan**</span><span class="sxs-lookup"><span data-stu-id="f410e-166">**background**</span></span>  
  <span data-ttu-id="f410e-167">Görevler, başlangıç rolünün ile paralel zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f410e-167">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span>
* <span data-ttu-id="f410e-168">**ön plan**</span><span class="sxs-lookup"><span data-stu-id="f410e-168">**foreground**</span></span>  
  <span data-ttu-id="f410e-169">Görevler, başlangıç rolünün ile paralel zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f410e-169">Tasks are executed asynchronously, in parallel with the startup of the role.</span></span> <span data-ttu-id="f410e-170">Arasındaki temel farklılık bir **ön plan** ve **arka plan** görev olan bir **ön plan** görev rol geri dönüştürme ya da görev sona erinceye kadar kapatılıyor engeller.</span><span class="sxs-lookup"><span data-stu-id="f410e-170">The key difference between a **foreground** and a **background** task is that a **foreground** task prevents the role from recycling or shutting down until the task has ended.</span></span> <span data-ttu-id="f410e-171">**Arka plan** görevleri bu kısıtlama yok.</span><span class="sxs-lookup"><span data-stu-id="f410e-171">The **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="f410e-172">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="f410e-172">Environment variables</span></span>
<span data-ttu-id="f410e-173">Ortam değişkenleri, bir başlangıç görevi bilgi aktarmak için bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="f410e-173">Environment variables are a way to pass information to a startup task.</span></span> <span data-ttu-id="f410e-174">Örneğin, yüklemek için bir programı içeren blob veya rolünüze kullanacağı bağlantı noktası numaraları ve başlangıç görevinin özelliklerini denetlemek için ayarları yolu koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f410e-174">For example, you can put the path to a blob that contains a program to install, or port numbers that your role will use, or settings to control features of your startup task.</span></span>

<span data-ttu-id="f410e-175">Başlangıç görevler için ortam değişkenleri iki tür vardır; statik ortam değişkenleri ve ortam değişkenleri göre üyelerinde [RoleEnvironment] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f410e-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of the [RoleEnvironment] class.</span></span> <span data-ttu-id="f410e-176">Her ikisi de bulunan [ortam] bölümünü [ServiceDefinition.csdef] dosya ve her iki kullanım [değişken] öğesi ve **adı** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f410e-176">Both are in the [Environment] section of the [ServiceDefinition.csdef] file, and both use the [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="f410e-177">Statik ortam değişkenlerini kullanır **değeri** özniteliği [değişken] öğesi.</span><span class="sxs-lookup"><span data-stu-id="f410e-177">Static environment variables uses the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="f410e-178">Yukarıdaki örnekte ortam değişkeni oluşturur **MyVersionNumber** statik değeri olan "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="f410e-178">The example above creates the environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="f410e-179">Başka bir örnek oluşturmak için olabilir bir **StagingOrProduction** değerleri el ile ayarlayabilirsiniz ortam değişkeni "**hazırlama**"veya"**üretim**" değerine göre farklı başlangıç eylemleri gerçekleştirmek için **StagingOrProduction** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f410e-179">Another example would be to create a **StagingOrProduction** environment variable which you can manually set to values of "**staging**" or "**production**" to perform different startup actions based on the value of the **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="f410e-180">RoleEnvironment sınıfının üyelere bağlı ortam değişkenlerini kullanma **değeri** özniteliği [değişken] öğesi.</span><span class="sxs-lookup"><span data-stu-id="f410e-180">Environment variables based on members of the RoleEnvironment class do not use the **value** attribute of the [Variable] element.</span></span> <span data-ttu-id="f410e-181">Bunun yerine, [RoleInstanceValue] uygun olan alt öğesi **XPath** öznitelik değeri, belirli bir üye üzerinde dayalı bir ortam değişkeni oluşturmak için kullanılan [RoleEnvironment] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f410e-181">Instead, the [RoleInstanceValue] child element, with the appropriate **XPath** attribute value, are used to create an environment variable based on a specific member of the [RoleEnvironment] class.</span></span> <span data-ttu-id="f410e-182">İçin değerler **XPath** çeşitli erişmek için öznitelik [RoleEnvironment] değerler bulunabilir [burada](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="f410e-182">Values for the **XPath** attribute to access various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="f410e-183">Örneğin, bir ortam değişkeni oluşturmak için "**true**" örneği için işlem öykünücüsünü çalıştırırken ve "**false**" bulutta çalıştırırken aşağıdaki kullanın [değişken] ve [RoleInstanceValue] öğeleri:</span><span class="sxs-lookup"><span data-stu-id="f410e-183">For example, to create an environment variable that is "**true**" when the instance is running in the compute emulator, and "**false**" when running in the cloud, use the following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create the environment variable that informs the startup task whether it is running
                in the Compute Emulator or in the cloud. "%ComputeEmulatorRunning%"=="true" when
                running in the Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in the cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="f410e-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f410e-184">Next steps</span></span>
<span data-ttu-id="f410e-185">Bazı gerçekleştirmek öğrenin [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md) bulut hizmetiniz ile.</span><span class="sxs-lookup"><span data-stu-id="f410e-185">Learn how to perform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="f410e-186">[Paket](cloud-services-model-and-package.md) bulut hizmetiniz.</span><span class="sxs-lookup"><span data-stu-id="f410e-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

<span data-ttu-id="f410e-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span><span class="sxs-lookup"><span data-stu-id="f410e-187">[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef</span></span>
<span data-ttu-id="f410e-188">[görev]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span><span class="sxs-lookup"><span data-stu-id="f410e-188">[Task]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task</span></span>
<span data-ttu-id="f410e-189">[başlangıç]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span><span class="sxs-lookup"><span data-stu-id="f410e-189">[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup</span></span>
<span data-ttu-id="f410e-190">[çalışma zamanı]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span><span class="sxs-lookup"><span data-stu-id="f410e-190">[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime</span></span>
<span data-ttu-id="f410e-191">[ortam]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span><span class="sxs-lookup"><span data-stu-id="f410e-191">[Environment]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment</span></span>
<span data-ttu-id="f410e-192">[değişken]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span><span class="sxs-lookup"><span data-stu-id="f410e-192">[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable</span></span>
<span data-ttu-id="f410e-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span><span class="sxs-lookup"><span data-stu-id="f410e-193">[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue</span></span>
<span data-ttu-id="f410e-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span><span class="sxs-lookup"><span data-stu-id="f410e-194">[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx</span></span>
