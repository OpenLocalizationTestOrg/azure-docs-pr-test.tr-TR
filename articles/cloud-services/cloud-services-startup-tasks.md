---
title: "aaaRun Azure Cloud Services başlangıç görevleri | Microsoft Docs"
description: "Başlangıç görevi, bulut hizmeti ortamınızı uygulamanız için hazırlanmanıza yardımcı. Bu iş başlangıç görevleri nasıl ve ne öğretilmektedir toomake bunları"
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
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a><span data-ttu-id="f977d-104">Nasıl tooconfigure ve çalıştırma başlangıç için bir bulut hizmeti görevleri</span><span class="sxs-lookup"><span data-stu-id="f977d-104">How tooconfigure and run startup tasks for a cloud service</span></span>
<span data-ttu-id="f977d-105">Bir rolü başlamadan önce başlangıç görevleri tooperform işlemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f977d-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="f977d-106">Bir bileşeni yüklemek, COM bileşenlerini kaydetme, kayıt defteri anahtarlarını ayarlamak veya uzun süre çalışan bir işlem başlatılıyor tooperform isteyebilirsiniz işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f977d-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span>

> [!NOTE]
> <span data-ttu-id="f977d-107">Başlangıç değil yalnızca tooCloud Service Web ve çalışan rolleri geçerli tooVirtual makineleri görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="f977d-107">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 
> 

## <a name="how-startup-tasks-work"></a><span data-ttu-id="f977d-108">Başlangıç görevi nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="f977d-108">How startup tasks work</span></span>
<span data-ttu-id="f977d-109">Başlangıç görevlerdir rollerinizi başlar ve hello tanımlanan önce gerçekleştirilen eylemler [ServiceDefinition.csdef] hello kullanarak dosya [görev] hello öğesinde [başlangıç]öğesi.</span><span class="sxs-lookup"><span data-stu-id="f977d-109">Startup tasks are actions that are taken before your roles begin and are defined in hello [ServiceDefinition.csdef] file by using hello [Task] element within hello [Startup] element.</span></span> <span data-ttu-id="f977d-110">Sık başlangıç görevleri toplu dosyalar, ancak bunlar aynı zamanda konsol uygulamaları veya PowerShell komut dosyalarını Başlat toplu iş dosyaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-110">Frequently startup tasks are batch files, but they can also be console applications, or batch files that start PowerShell scripts.</span></span>

<span data-ttu-id="f977d-111">Ortam değişkenleri, bir başlangıç görevi bilgi aktarmak ve yerel depolama bir başlangıç görevi dışında kullanılan toopass bilgi olabilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-111">Environment variables pass information into a startup task, and local storage can be used toopass information out of a startup task.</span></span> <span data-ttu-id="f977d-112">Örneğin, bir ortam değişkeni hello yolu tooa program belirtebilirsiniz tooinstall istediğiniz ve ardından daha sonra rolleri tarafından okunabilir toolocal depolama dosyaları yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-112">For example, an environment variable can specify hello path tooa program you want tooinstall, and files can be written toolocal storage that can then be read later by your roles.</span></span>

<span data-ttu-id="f977d-113">Başlangıç görevi bilgileri ve hello tarafından belirtilen hataları toohello dizin oturum **TEMP** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f977d-113">Your startup task can log information and errors toohello directory specified by hello **TEMP** environment variable.</span></span> <span data-ttu-id="f977d-114">Merhaba başlangıç görevi sırasında hello **TEMP** ortam değişkenini çözümler toohello *C:\\kaynakları\\temp\\[GUID]. [ Rol adı]\\RoleTemp* hello bulut üzerinde çalışırken dizin.</span><span class="sxs-lookup"><span data-stu-id="f977d-114">During hello startup task, hello **TEMP** environment variable resolves toohello *C:\\Resources\\temp\\[guid].[rolename]\\RoleTemp* directory when running on hello cloud.</span></span>

<span data-ttu-id="f977d-115">Başlangıç görevi yeniden başlatmalar arasında da birkaç kez çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-115">Startup tasks can also be executed several times between reboots.</span></span> <span data-ttu-id="f977d-116">Örneğin, hello başlangıç görevi hello rol geri dönüştürme her zaman çalıştırılır ve rol dönüştürür her zaman yeniden başlatma içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-116">For example, hello startup task will be run each time hello role recycles, and role recycles may not always include a reboot.</span></span> <span data-ttu-id="f977d-117">Başlangıç görevi sorunsuz birkaç kez toorun tanır şekilde yazılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f977d-117">Startup tasks should be written in a way that allows them toorun several times without problems.</span></span>

<span data-ttu-id="f977d-118">Başlangıç görevleri ile bitmelidir bir **errorlevel** (veya çıkış kodu) hello başlatma işlemi toocomplete sıfır.</span><span class="sxs-lookup"><span data-stu-id="f977d-118">Startup tasks must end with an **errorlevel** (or exit code) of zero for hello startup process toocomplete.</span></span> <span data-ttu-id="f977d-119">Bir başlangıç görevi bir sıfır ile bitip bitmediğini **errorlevel**, hello rol başlatılmayacak.</span><span class="sxs-lookup"><span data-stu-id="f977d-119">If a startup task ends with a non-zero **errorlevel**, hello role will not start.</span></span>

## <a name="role-startup-order"></a><span data-ttu-id="f977d-120">Rol başlatma sırası</span><span class="sxs-lookup"><span data-stu-id="f977d-120">Role startup order</span></span>
<span data-ttu-id="f977d-121">Aşağıdaki listeler hello rol başlatma yordamı azure'da hello:</span><span class="sxs-lookup"><span data-stu-id="f977d-121">hello following lists hello role startup procedure in Azure:</span></span>

1. <span data-ttu-id="f977d-122">Merhaba örneği olarak işaretli **başlangıç** ve trafik almaz.</span><span class="sxs-lookup"><span data-stu-id="f977d-122">hello instance is marked as **Starting** and does not receive traffic.</span></span>
2. <span data-ttu-id="f977d-123">Tüm başlangıç görevleri tootheir göre yürütülür **taskType** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f977d-123">All startup tasks are executed according tootheir **taskType** attribute.</span></span>
   
   * <span data-ttu-id="f977d-124">Merhaba **basit** görevler eşzamanlı olarak, yürütülen bir kerede.</span><span class="sxs-lookup"><span data-stu-id="f977d-124">hello **simple** tasks are executed synchronously, one at a time.</span></span>
   * <span data-ttu-id="f977d-125">Merhaba **arka plan** ve **ön plan** zaman uyumsuz olarak başlatılan, paralel toohello başlangıç görevi görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="f977d-125">hello **background** and **foreground** tasks are started asynchronously, parallel toohello startup task.</span></span>  
     
     > [!WARNING]
     > <span data-ttu-id="f977d-126">Role özgü verileri kullanılabilir olmaması IIS tam olarak hello başlatma işleminde hello başlangıç görevi aşaması sırasında yapılandırılmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-126">IIS may not be fully configured during hello startup task stage in hello startup process, so role-specific data may not be available.</span></span> <span data-ttu-id="f977d-127">Role özgü veri gerektiren başlangıç görevleri kullanması gereken [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span><span class="sxs-lookup"><span data-stu-id="f977d-127">Startup tasks that require role-specific data should use [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).</span></span>
     > 
     > 
3. <span data-ttu-id="f977d-128">Hello rol ana bilgisayar işlemi başlatıldı ve hello sitesi IIS içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f977d-128">hello role host process is started and hello site is created in IIS.</span></span>
4. <span data-ttu-id="f977d-129">Merhaba [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="f977d-129">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method is called.</span></span>
5. <span data-ttu-id="f977d-130">Merhaba örneği olarak işaretli **hazır** ve trafik yönlendirilmiş toohello örneği.</span><span class="sxs-lookup"><span data-stu-id="f977d-130">hello instance is marked as **Ready** and traffic is routed toohello instance.</span></span>
6. <span data-ttu-id="f977d-131">Merhaba [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="f977d-131">hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method is called.</span></span>

## <a name="example-of-a-startup-task"></a><span data-ttu-id="f977d-132">Bir başlangıç görevi örneği</span><span class="sxs-lookup"><span data-stu-id="f977d-132">Example of a startup task</span></span>
<span data-ttu-id="f977d-133">Başlangıç görevi hello tanımlanmış [ServiceDefinition.csdef] dosyasında hello **görev** öğesi.</span><span class="sxs-lookup"><span data-stu-id="f977d-133">Startup tasks are defined in hello [ServiceDefinition.csdef] file, in hello **Task** element.</span></span> <span data-ttu-id="f977d-134">Merhaba **commandLine** özniteliği hello adını belirtir ve hello başlangıç toplu parametrelerinin dosya veya komut, hello konsol **executionContext** özniteliği belirtir hello başlangıç hello ayrıcalık düzeyi Görev ve hello **taskType** özniteliği belirtir nasıl hello görev yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f977d-134">hello **commandLine** attribute specifies hello name and parameters of hello startup batch file or console command, hello **executionContext** attribute specifies hello privilege level of hello startup task, and hello **taskType** attribute specifies how hello task will be executed.</span></span>

<span data-ttu-id="f977d-135">Bu örnekte, bir ortam değişkeni **MyVersionNumber**, hello başlangıç görevi için oluşturulan ve toohello değerini "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="f977d-135">In this example, an environment variable, **MyVersionNumber**, is created for hello startup task and set toohello value "**1.0.0.0**".</span></span>

<span data-ttu-id="f977d-136">**ServiceDefinition.csdef**:</span><span class="sxs-lookup"><span data-stu-id="f977d-136">**ServiceDefinition.csdef**:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

<span data-ttu-id="f977d-137">Aşağıdaki örneğine hello hello **Startup.cmd** toplu iş dosyası hello TEMP ortam değişkeni tarafından belirtilen hello dizininde "Merhaba geçerli sürüm 1.0.0.0" toohello StartupLog.txt dosyası hello satır yazar.</span><span class="sxs-lookup"><span data-stu-id="f977d-137">In hello following example, hello **Startup.cmd** batch file writes hello line "hello current version is 1.0.0.0" toohello StartupLog.txt file in hello directory specified by hello TEMP environment variable.</span></span> <span data-ttu-id="f977d-138">Merhaba `EXIT /B 0` satır sağlar, hello başlangıç görevi sonlandırır ile bir **errorlevel** sıfır.</span><span class="sxs-lookup"><span data-stu-id="f977d-138">hello `EXIT /B 0` line ensures that hello startup task ends with an **errorlevel** of zero.</span></span>

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> <span data-ttu-id="f977d-139">Visual Studio'da hello **tooOutput dizin kopyalama** özelliği başlangıç toplu işlem dosyanız için çok ayarlanmalıdır**her zaman Kopyala** toobe başlangıç toplu iş dosyası doğru olduğundan emin dağıtılan Azure tooyour projede (**approot\\bin** Web rolleri için ve **approot** çalışan roller için).</span><span class="sxs-lookup"><span data-stu-id="f977d-139">In Visual Studio, hello **Copy tooOutput Directory** property for your startup batch file should be set too**Copy Always** toobe sure that your startup batch file is properly deployed tooyour project on Azure (**approot\\bin** for Web roles, and **approot** for worker roles).</span></span>
> 
> 

## <a name="description-of-task-attributes"></a><span data-ttu-id="f977d-140">Görev öznitelikler açıklaması</span><span class="sxs-lookup"><span data-stu-id="f977d-140">Description of task attributes</span></span>
<span data-ttu-id="f977d-141">Merhaba aşağıdaki hello özniteliklerini hello açıklayan **görev** hello öğesinde [ServiceDefinition.csdef] dosyası:</span><span class="sxs-lookup"><span data-stu-id="f977d-141">hello following describes hello attributes of hello **Task** element in hello [ServiceDefinition.csdef] file:</span></span>

<span data-ttu-id="f977d-142">**komut satırı** -hello başlangıç görevi için hello komut satırını belirtir:</span><span class="sxs-lookup"><span data-stu-id="f977d-142">**commandLine** - Specifies hello command line for hello startup task:</span></span>

* <span data-ttu-id="f977d-143">Merhaba başlangıç görevi başlatan hello komutuyla, isteğe bağlı komut satırı parametreleri.</span><span class="sxs-lookup"><span data-stu-id="f977d-143">hello command, with optional command line parameters, which begins hello startup task.</span></span>
* <span data-ttu-id="f977d-144">Sık hello filename .cmd veya .bat toplu iş dosyası budur.</span><span class="sxs-lookup"><span data-stu-id="f977d-144">Frequently this is hello filename of a .cmd or .bat batch file.</span></span>
* <span data-ttu-id="f977d-145">Merhaba görevdir göreli toohello AppRoot\\Bin klasörü hello dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="f977d-145">hello task is relative toohello AppRoot\\Bin folder for hello deployment.</span></span> <span data-ttu-id="f977d-146">Ortam değişkenleri hello yolu ve dosya hello görevinin belirlerken genişletilir değil.</span><span class="sxs-lookup"><span data-stu-id="f977d-146">Environment variables are not expanded in determining hello path and file of hello task.</span></span> <span data-ttu-id="f977d-147">Ortam genişletme gerekiyorsa, başlangıç görevi çağıran bir küçük .cmd komut dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f977d-147">If environment expansion is required, you can create a small .cmd script that calls your startup task.</span></span>
* <span data-ttu-id="f977d-148">Bir konsol uygulaması ya da başlayan bir toplu iş dosyası bir [PowerShell Betiği](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span><span class="sxs-lookup"><span data-stu-id="f977d-148">Can be a console application or a batch file that starts a [PowerShell script](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).</span></span>

<span data-ttu-id="f977d-149">**executionContext** -hello başlangıç görevi hello ayrıcalık düzeyini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f977d-149">**executionContext** - Specifies hello privilege level for hello startup task.</span></span> <span data-ttu-id="f977d-150">Merhaba ayrıcalık düzeyi sınırlı veya yükseltilmiş:</span><span class="sxs-lookup"><span data-stu-id="f977d-150">hello privilege level can be limited or elevated:</span></span>

* <span data-ttu-id="f977d-151">**sınırlı**</span><span class="sxs-lookup"><span data-stu-id="f977d-151">**limited**</span></span>  
  <span data-ttu-id="f977d-152">aynı hello rolü olarak ayrıcalıkları hello ile Merhaba başlangıç görevi çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f977d-152">hello startup task runs with hello same privileges as hello role.</span></span> <span data-ttu-id="f977d-153">Ne zaman hello **executionContext** özniteliği hello için [çalışma zamanı] öğesidir de **sınırlı**, kullanıcı ayrıcalıkları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f977d-153">When hello **executionContext** attribute for hello [Runtime] element is also **limited**, then user privileges are used.</span></span>
* <span data-ttu-id="f977d-154">**yükseltilmiş**</span><span class="sxs-lookup"><span data-stu-id="f977d-154">**elevated**</span></span>  
  <span data-ttu-id="f977d-155">Merhaba başlangıç görevi yönetici ayrıcalıklarıyla çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f977d-155">hello startup task runs with administrator privileges.</span></span> <span data-ttu-id="f977d-156">Bu başlangıç görevleri tooinstall programları sağlar, IIS yapılandırma değişiklikleri, hello ayrıcalık düzeyi hello rolünün kendisini artırmadan kayıt defteri değişikliklerini ve diğer yönetici düzeyi görevleri gerçekleştirmek.</span><span class="sxs-lookup"><span data-stu-id="f977d-156">This allows startup tasks tooinstall programs, make IIS configuration changes, perform registry changes, and other administrator level tasks, without increasing hello privilege level of hello role itself.</span></span>  

> [!NOTE]
> <span data-ttu-id="f977d-157">Merhaba ayrıcalık düzeyi başlangıç görevinin ihtiyaç duymadığı toobe hello aynı hello rolü olarak kendisi.</span><span class="sxs-lookup"><span data-stu-id="f977d-157">hello privilege level of a startup task does not need toobe hello same as hello role itself.</span></span>
> 
> 

<span data-ttu-id="f977d-158">**taskType** -hello şekilde bir başlangıç görevi yürütüldüğünde belirtir.</span><span class="sxs-lookup"><span data-stu-id="f977d-158">**taskType** - Specifies hello way a startup task is executed.</span></span>

* <span data-ttu-id="f977d-159">**Basit**</span><span class="sxs-lookup"><span data-stu-id="f977d-159">**simple**</span></span>  
  <span data-ttu-id="f977d-160">Görevlerin yürütülme eşzamanlı olarak, bir kerede, hello sırayla hello belirtilen [ServiceDefinition.csdef] dosya.</span><span class="sxs-lookup"><span data-stu-id="f977d-160">Tasks are executed synchronously, one at a time, in hello order specified in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="f977d-161">Bir zaman **basit** başlangıç görevi sonlandırır ile bir **errorlevel** hiç biri, sonraki hello **basit** başlangıç görevi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-161">When one **simple** startup task ends with an **errorlevel** of zero, hello next **simple** startup task is executed.</span></span> <span data-ttu-id="f977d-162">Artık böyle olduğunda **basit** başlangıç görevleri tooexecute, sonra da hello rol kendisi başlatılır.</span><span class="sxs-lookup"><span data-stu-id="f977d-162">If there are no more **simple** startup tasks tooexecute, then hello role itself will be started.</span></span>   
  
  > [!NOTE]
  > <span data-ttu-id="f977d-163">Merhaba, **basit** görev bir sıfır ile biten **errorlevel**, hello örneği engellenir.</span><span class="sxs-lookup"><span data-stu-id="f977d-163">If hello **simple** task ends with a non-zero **errorlevel**, hello instance will be blocked.</span></span> <span data-ttu-id="f977d-164">Sonraki **basit** başlangıç görevleri ve hello rol kendisinin başlatılmayacak.</span><span class="sxs-lookup"><span data-stu-id="f977d-164">Subsequent **simple** startup tasks, and hello role itself, will not start.</span></span>
  > 
  > 
  
    <span data-ttu-id="f977d-165">Toplu iş dosyası ile biten tooensure bir **errorlevel** hiç biri hello bağlamını `EXIT /B 0` toplu iş dosyası işleminizi hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="f977d-165">tooensure that your batch file ends with an **errorlevel** of zero, execute hello command `EXIT /B 0` at hello end of your batch file process.</span></span>
* <span data-ttu-id="f977d-166">**arka plan**</span><span class="sxs-lookup"><span data-stu-id="f977d-166">**background**</span></span>  
  <span data-ttu-id="f977d-167">Görevler hello başlangıç hello rolünün ile paralel zaman uyumsuz olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="f977d-167">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span>
* <span data-ttu-id="f977d-168">**ön plan**</span><span class="sxs-lookup"><span data-stu-id="f977d-168">**foreground**</span></span>  
  <span data-ttu-id="f977d-169">Görevler hello başlangıç hello rolünün ile paralel zaman uyumsuz olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="f977d-169">Tasks are executed asynchronously, in parallel with hello startup of hello role.</span></span> <span data-ttu-id="f977d-170">Merhaba arasındaki temel farklılık bir **ön plan** ve **arka plan** görev olan bir **ön plan** görev engeller hello rol geri dönüştürme veya hello görev olana kadar kapatılıyor sona erdi.</span><span class="sxs-lookup"><span data-stu-id="f977d-170">hello key difference between a **foreground** and a **background** task is that a **foreground** task prevents hello role from recycling or shutting down until hello task has ended.</span></span> <span data-ttu-id="f977d-171">Merhaba **arka plan** görevleri bu kısıtlama yok.</span><span class="sxs-lookup"><span data-stu-id="f977d-171">hello **background** tasks do not have this restriction.</span></span>

## <a name="environment-variables"></a><span data-ttu-id="f977d-172">Ortam değişkenleri</span><span class="sxs-lookup"><span data-stu-id="f977d-172">Environment variables</span></span>
<span data-ttu-id="f977d-173">Ortam değişkenleri bir şekilde toopass bilgi tooa başlangıç görevi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f977d-173">Environment variables are a way toopass information tooa startup task.</span></span> <span data-ttu-id="f977d-174">Örneğin, bir program tooinstall içeren hello yolu tooa blob veya rolünüze kullanacağı bağlantı noktası numaralarını veya ayarları toocontrol özellikleri, başlangıç görevinin koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f977d-174">For example, you can put hello path tooa blob that contains a program tooinstall, or port numbers that your role will use, or settings toocontrol features of your startup task.</span></span>

<span data-ttu-id="f977d-175">Başlangıç görevler için ortam değişkenleri iki tür vardır; statik ortam değişkenleri ve ortam değişkenleri göre hello üyelerinde [ RoleEnvironment] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f977d-175">There are two kinds of environment variables for startup tasks; static environment variables and environment variables based on members of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="f977d-176">Her ikisi de hello olan [ortam] hello bölümünü [ServiceDefinition.csdef] dosya ve her iki kullanım hello [değişken] öğesi ve **adı** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f977d-176">Both are in hello [Environment] section of hello [ServiceDefinition.csdef] file, and both use hello [Variable] element and **name** attribute.</span></span>

<span data-ttu-id="f977d-177">Statik ortam değişkenlerini kullanır hello **değeri** hello özniteliği [değişken] öğesi.</span><span class="sxs-lookup"><span data-stu-id="f977d-177">Static environment variables uses hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="f977d-178">Yukarıdaki Hello örneği oluşturur hello ortam değişkeni **MyVersionNumber** statik değeri olan "**1.0.0.0**".</span><span class="sxs-lookup"><span data-stu-id="f977d-178">hello example above creates hello environment variable **MyVersionNumber** which has a static value of "**1.0.0.0**".</span></span> <span data-ttu-id="f977d-179">Başka bir örnek toocreate olabilir bir **StagingOrProduction** toovalues, el ile ayarlayabilirsiniz ortam değişkeni "**hazırlama**"veya"**üretim**" tooperform farklı bir başlangıç Eylemler dayalı hello hello değerini **StagingOrProduction** ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="f977d-179">Another example would be toocreate a **StagingOrProduction** environment variable which you can manually set toovalues of "**staging**" or "**production**" tooperform different startup actions based on hello value of hello **StagingOrProduction** environment variable.</span></span>

<span data-ttu-id="f977d-180">Ortam değişkenleri hello RoleEnvironment sınıfı üyelerinde dayalı hello kullanmayın **değeri** hello özniteliği [değişken] öğesi.</span><span class="sxs-lookup"><span data-stu-id="f977d-180">Environment variables based on members of hello RoleEnvironment class do not use hello **value** attribute of hello [Variable] element.</span></span> <span data-ttu-id="f977d-181">Bunun yerine, hello [RoleInstanceValue] hello uygun olan alt öğesi **XPath** öznitelik değeri, belirli bir hello üyede dayalı bir ortam değişkeni kullanılan toocreate olan [ RoleEnvironment] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f977d-181">Instead, hello [RoleInstanceValue] child element, with hello appropriate **XPath** attribute value, are used toocreate an environment variable based on a specific member of hello [RoleEnvironment] class.</span></span> <span data-ttu-id="f977d-182">Merhaba değerlerini **XPath** tooaccess çeşitli öznitelik [ RoleEnvironment] değerler bulunabilir [burada](cloud-services-role-config-xpath.md).</span><span class="sxs-lookup"><span data-stu-id="f977d-182">Values for hello **XPath** attribute tooaccess various [RoleEnvironment] values can be found [here](cloud-services-role-config-xpath.md).</span></span>

<span data-ttu-id="f977d-183">Örneğin, toocreate olan bir ortam değişkeni "**true**" Merhaba örneği hello işlem öykünücüsünde çalıştırırken ve "**false**" Merhaba bulutta çalıştırırken hello aşağıdaki kullanın [değişken] ve [RoleInstanceValue] öğeleri:</span><span class="sxs-lookup"><span data-stu-id="f977d-183">For example, toocreate an environment variable that is "**true**" when hello instance is running in hello compute emulator, and "**false**" when running in hello cloud, use hello following [Variable] and [RoleInstanceValue] elements:</span></span>

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a><span data-ttu-id="f977d-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f977d-184">Next steps</span></span>
<span data-ttu-id="f977d-185">Bilgi nasıl tooperform bazı [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md) bulut hizmetiniz ile.</span><span class="sxs-lookup"><span data-stu-id="f977d-185">Learn how tooperform some [common startup tasks](cloud-services-startup-tasks-common.md) with your Cloud Service.</span></span>

<span data-ttu-id="f977d-186">[Paket](cloud-services-model-and-package.md) bulut hizmetiniz.</span><span class="sxs-lookup"><span data-stu-id="f977d-186">[Package](cloud-services-model-and-package.md) your Cloud Service.</span></span>  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[görev]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[başlangıç]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[çalışma zamanı]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ortam]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[değişken]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
