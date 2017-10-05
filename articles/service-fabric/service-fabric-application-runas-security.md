---
title: "Azure mikro güvenlik ilkeleri hakkında bilgi edinin | Microsoft Docs"
description: "Bir Service Fabric uygulaması sistem ve yerel güvenlik hesaplarını, burada bir uygulama başlatılmadan önce bazı ayrıcalıklı eylemleri gerçekleştirmek için gereken SetupEntry noktası dahil altında çalıştırmak nasıl bir genel bakış"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: e673b45a43a06d18040c3437caf8765704d5c36a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="c4dbf-103">Uygulamanıza yönelik güvenlik ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4dbf-103">Configure security policies for your application</span></span>
<span data-ttu-id="c4dbf-104">Azure Service Fabric kullanarak, kümedeki farklı kullanıcı hesabı altında çalışan uygulamaları güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-104">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="c4dbf-105">Service Fabric uygulamaları tarafından kullanıcı hesapları altında--dağıtım zamanında örneğin kullanılan kaynaklar, dosyaları, dizinleri ve sertifikaları güvenli yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="c4dbf-106">Bu çalışan uygulamaları bile paylaşılan bir barındırılan ortamda, diğerinden daha güvenli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="c4dbf-107">Varsayılan olarak, Service Fabric uygulamaları Fabric.exe işlemin altında çalıştığı hesap altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="c4dbf-108">Service Fabric de bir yerel kullanıcı hesabı veya uygulama bildirimi içinde belirtilen yerel sistem hesabı altında uygulamaları çalıştırmak için yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="c4dbf-109">Desteklenen yerel sistem hesabı türleri **YerelKullanıcı**, **NetworkService**, **Yerelhizmet**, ve **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="c4dbf-110">Tek başına yükleyici kullanarak, veri merkezinizde Windows Server'da Service Fabric çalıştırıyorsanız, Grup yönetilen hizmet hesapları dahil olmak üzere Active Directory etki alanı hesaplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="c4dbf-111">Tanımlayabilir ve kullanıcı grupları oluşturun, böylece bir veya daha fazla kullanıcı birlikte yönetilecek her gruba eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="c4dbf-112">Bu, farklı hizmet giriş noktaları için birden çok kullanıcı ve grup düzeyinde kullanılabilen bazı ortak ayrıcalıklarına sahip olmanız gerekir yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="c4dbf-113">Bir hizmet Kurulum giriş noktası için ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4dbf-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="c4dbf-114">Bölümünde açıklandığı gibi [uygulama modeli](service-fabric-application-model.md), Kurulum giriş noktası **SetupEntryPoint**, Service Fabric kimlik bilgileriyle çalışır ayrıcalıklı giriş noktasıdır (genellikle  *NetworkService* hesabı) önce başka bir giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="c4dbf-115">Tarafından belirtilen yürütülebilir dosya **EntryPoint** genellikle uzun süre çalışan hizmet yöneticisidir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="c4dbf-116">Bu nedenle ayrı Kurulum giriş noktası sahip hizmet ana bilgisayarı yürütülebilir yüksek ayrıcalıklara sahip genişletilmiş süre için çalıştırmanız gereğini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="c4dbf-117">Yürütülebilir dosya, **EntryPoint** belirtir çalıştırıldıktan **SetupEntryPoint** başarıyla çıkar.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="c4dbf-118">Sonuçta elde edilen işlem izlenen ve yeniden başlatılabilir ve yeniden ile başlayan **SetupEntryPoint** hiç sonlandırır veya çöküyor.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="c4dbf-119">SetupEntryPoint ve hizmet için ana EntryPoint gösteren basit hizmeti bildirim bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="c4dbf-120">Yerel bir hesap kullanarak ilkeyi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4dbf-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="c4dbf-121">Kurulum giriş noktası için hizmet yapılandırdıktan sonra uygulama bildiriminde altında çalıştığı güvenlik izinlerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="c4dbf-122">Aşağıdaki örnekte, kullanıcı yönetici hesabının ayrıcalıklarını altında çalışacağı hizmetin yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

<span data-ttu-id="c4dbf-123">İlk olarak, oluşturma bir **sorumluları** SetupAdminUser gibi bir kullanıcı adı bölümü.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="c4dbf-124">Bu, kullanıcının yöneticiler sistem grubunun bir üyesi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="c4dbf-125">Sonraki altında **ServiceManifestImport** bölümünde, bu asıl uygulamak için bir ilke yapılandırın **SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="c4dbf-126">Bu Service Fabric gerektiğini bildirir **MySetup.bat** dosyasını çalıştırın, olmalıdır `RunAs` yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="c4dbf-127">Sahip olduğunuz o *değil* kodda ana giriş noktası için bir ilke uygulanmış **MyServiceHost.exe** sisteminde çalışıyor **NetworkService** hesabı.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="c4dbf-128">Bu, tüm hizmet giriş noktaları olarak çalıştırılan varsayılan hesaptır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="c4dbf-129">Artık dosya MySetup.bat yönetici ayrıcalıklarını test etmek için Visual Studio projesi ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="c4dbf-130">Visual Studio'da hizmet projesine sağ tıklayın ve MySetup.bat adlı yeni bir dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="c4dbf-131">Ardından, MySetup.bat dosya hizmet paketinde bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="c4dbf-132">Varsayılan olarak, bu değil.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-132">By default, it is not.</span></span> <span data-ttu-id="c4dbf-133">Dosya seçin, bağlam menüsü almak için sağ tıklatın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="c4dbf-134">Özellikler iletişim kutusunda emin **çıktı dizinine Kopyala** ayarlanır **yeniyse Kopyala**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="c4dbf-135">Aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-135">See the following screenshot.</span></span>

![SetupEntryPoint toplu iş dosyası için Visual Studio CopyToOutput][image1]

<span data-ttu-id="c4dbf-137">Şimdi MySetup.bat dosyasını açın ve aşağıdaki komutları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="c4dbf-138">Ardından, yapı ve bir yerel geliştirme kümeye çözümü dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="c4dbf-139">Service Fabric Explorer'da gösterildiği gibi hizmet başladıktan sonra MySetup.bat dosyasını iki yolla başarılı olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="c4dbf-140">Bir PowerShell komut istemi açıp türü:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="c4dbf-141">Ardından, burada hizmet dağıtıldı ve Service Fabric Explorer'da--Örneğin, düğüm 2 başlatılan düğüm adını not edin.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="c4dbf-142">Ardından, değerini gösterir out.txt dosyayı bulmak için uygulama örnek iş klasöre gidin **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="c4dbf-143">Bu hizmet düğümü 2'ye dağıttıysanız, örneğin, ardından bu yol için gidebilirsiniz **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="c4dbf-144">Yerel Sistem hesapları kullanarak ilkeyi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4dbf-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="c4dbf-145">Genellikle, bir yönetici hesabı yerine yerel sistem hesabı kullanarak başlangıç komut dosyasını çalıştırmak için tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="c4dbf-146">İyi makineler kullanıcı erişim denetimi (UAC) varsayılan olarak etkin olduğundan, genellikle RunAs ilke Yöneticiler grubunun bir üyesi olarak çalışan işe yaramaz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="c4dbf-147">Böyle durumlarda, **SetupEntryPoint LocalSystem olarak yerine Yöneticiler grubuna eklenmiş yerel bir kullanıcı olarak çalıştırmak için önerilir**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="c4dbf-148">Aşağıdaki örnek, LocalSystem olarak çalışacak şekilde SetupEntryPoint ayarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="c4dbf-149">PowerShell komutlarını bir Kurulum giriş noktasından Başlat</span><span class="sxs-lookup"><span data-stu-id="c4dbf-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="c4dbf-150">Powershell'den çalıştırmak için **SetupEntryPoint** noktası çalıştırabilirsiniz **PowerShell.exe** bir toplu iş dosyasında bir PowerShell dosyasını işaret eder.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="c4dbf-151">İlk olarak, bir PowerShell dosya hizmeti projesine--Örneğin, ekleyin **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="c4dbf-152">Ayarlamayı unutmayın *yeniyse Kopyala* özelliği böylece dosyayı Ayrıca hizmet paketinde dahil.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="c4dbf-153">Adlı Sistem ortam değişkenini ayarlar MySetup.ps1 adlı bir PowerShell dosya başlatır örnek bir toplu iş dosyası aşağıdaki örnekte **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="c4dbf-154">PowerShell dosyası başlatmak için MySetup.bat:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="c4dbf-155">PowerShell dosyasında bir sistem ortam değişkenini ayarlamak üzere aşağıdakini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="c4dbf-156">Varsayılan olarak, toplu iş dosyası çalıştığında, uygulama klasörü adlı göründüğünü **iş** dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="c4dbf-157">MySetup.bat çalıştığında, bu durumda, bu uygulama aynı klasörde MySetup.ps1 dosyasını bulmak için istiyoruz **kod paketi** klasör.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="c4dbf-158">Bu klasörü değiştirmek için çalışma klasörü ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-158">To change this folder, set the working folder:</span></span>
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="c4dbf-159">Yerel hata ayıklama için konsolu yeniden yönlendirmeyi kullanma</span><span class="sxs-lookup"><span data-stu-id="c4dbf-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="c4dbf-160">Bazen, bir komut dosyası hata ayıklama amacıyla çalışmasını konsol çıkışı görmek yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="c4dbf-161">Bunu yapmak için çıktıyı bir dosyaya yazar konsol yeniden yönlendirme ilkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="c4dbf-162">Dosya çıktısı adlı uygulama klasörüne yazılır **günlük** düğümünde burada uygulamanın dağıtıldığı ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="c4dbf-163">(Bu önceki örnekte nerede bulacağını bakın.)</span><span class="sxs-lookup"><span data-stu-id="c4dbf-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="c4dbf-164">Hiçbir zaman bu uygulamayı yük devretme etkileyebileceğinden üretimde dağıtılan bir uygulamada konsol yeniden yönlendirme ilkesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="c4dbf-165">*Yalnızca* bunu yerel geliştirme ve hata ayıklama amacıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="c4dbf-166">Aşağıdaki örnek, konsol yeniden yönlendirmesi FileRetentionCount değeriyle ayarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="c4dbf-167">Şimdi yazmak için MySetup.ps1 dosyasını değiştirirseniz, bir **Echo** komutu, bu hata ayıklama amacıyla çıktı dosyasına yazacak:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="c4dbf-168">**Bu konsol yeniden yönlendirme ilkesi, komut dosyası hata ayıklama sonra hemen kaldırın**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="c4dbf-169">Hizmet kodu paketleri için bir ilke yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4dbf-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="c4dbf-170">Önceki adımlarda bir RunAs ilkesi uygulamak için SetupEntryPoint öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="c4dbf-171">Hizmeti ilkeleri uygulanabilecek farklı ilkeleri oluşturmak nasıl içine biraz daha derin bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="c4dbf-172">Yerel kullanıcı grupları oluşturun</span><span class="sxs-lookup"><span data-stu-id="c4dbf-172">Create local user groups</span></span>
<span data-ttu-id="c4dbf-173">Bir gruba eklenecek bir veya daha fazla kullanıcıların kullanıcı grupları oluşturun ve tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="c4dbf-174">Bu, farklı hizmet giriş noktaları için birden çok kullanıcı ve grup düzeyinde kullanılabilen bazı ortak ayrıcalıklara sahip olması gerekir yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-174">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="c4dbf-175">Aşağıdaki örnek adlı bir yerel Grup gösterir **LocalAdminGroup** yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="c4dbf-176">İki kullanıcılar, Customer1 ve Customer2, bu yerel grubun üyesi yapılır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a><span data-ttu-id="c4dbf-177">Yerel kullanıcılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4dbf-177">Create local users</span></span>
<span data-ttu-id="c4dbf-178">Uygulamasında bir hizmeti güvenli hale getirmek için kullanılan yerel bir kullanıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="c4dbf-179">Zaman bir **YerelKullanıcı** hesap türü belirtilen uygulama bildirimi ilkeleri bölümünde Service Fabric, uygulamanın dağıtıldığı makinelerde yerel kullanıcı hesaplarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="c4dbf-180">Varsayılan olarak, bu hesapları (örneğin, aşağıdaki örnekte Customer3) uygulama bildiriminde belirtilenlerle aynı adı yok.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="c4dbf-181">Bunun yerine, dinamik olarak oluşturulur ve rastgele parolalara sahip.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="c4dbf-182">Uygulamanın kullanıcı hesabı ve parolası (örneğin, için NTLM kimlik doğrulamasını etkinleştir) tüm makinelerde aynı gerektiriyorsa, küme bildiriminde NTLMAuthenticationEnabled true olarak ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="c4dbf-183">Küme bildiriminde tüm makinelerde aynı parola oluşturmak için kullanılan bir NTLMAuthenticationPasswordSecret de belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="c4dbf-184">Hizmet kodu paketler ilke ataması</span><span class="sxs-lookup"><span data-stu-id="c4dbf-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="c4dbf-185">**RunAsPolicy** bölümünde bir **ServiceManifestImport** kod paketi çalıştırmak için kullanılması gereken sorumluları bölümünden hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="c4dbf-186">Ayrıca ilkeleri bölümünde kullanıcı hesapları olan hizmet bildirimi kod paketi ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="c4dbf-187">Bu kurulum veya ana giriş noktaları için belirtebilirsiniz veya belirtebilirsiniz `All` her ikisini de uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="c4dbf-188">Aşağıdaki örnek, uygulanmakta olan farklı ilkeleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="c4dbf-189">Varsa **EntryPointType** belirtilmezse, varsayılan olarak EntryPointType için ayarlanmış "Ana" =.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="c4dbf-190">Belirtme **SetupEntryPoint** belirli yüksek ayrıcalıklı kurulum işlemlerini sistem hesabı altında çalıştırmak istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="c4dbf-191">Gerçek servis kodu düşük ayrıcalıklı hesap altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="c4dbf-192">Varsayılan bir ilke tüm hizmet kod paketleri için geçerlidir</span><span class="sxs-lookup"><span data-stu-id="c4dbf-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="c4dbf-193">Kullandığınız **DefaultRunAsPolicy** bölüm tüm kodları için varsayılan bir kullanıcı hesabı paketleri belirtmek için belirli bir sahip değilseniz **RunAsPolicy** tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="c4dbf-194">Bir uygulama tarafından kullanılan hizmet bildiriminde belirtilen kod paketleri çoğunu aynı kullanıcı altında çalıştırmanız gerekiyorsa, uygulamayı yalnızca bu kullanıcı hesabıyla varsayılan bir RunAs ilkesi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="c4dbf-195">Kod paketi yoksa belirleyen aşağıdaki örnekte bir **RunAsPolicy** belirtilen kod paketi altında çalışması gereken **MyDefaultAccount** ilkeleri bölümünde belirtilen.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="c4dbf-196">Bir Active Directory etki alanı grubu veya kullanıcı kullanın</span><span class="sxs-lookup"><span data-stu-id="c4dbf-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="c4dbf-197">Tek başına yükleyici kullanarak Windows sunucusuna yüklenen Service Fabric bir örneği için bir Active Directory kullanıcı veya grup hesabı için kimlik bilgileri altında hizmeti çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="c4dbf-198">Bu içi etki alanınızda Active Directory ve Azure Active Directory (Azure AD) değil.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c4dbf-199">Bir etki alanı kullanıcısı veya grubu kullanarak izinleri verilmiş olması (örneğin, dosya paylaşımları) etki alanındaki diğer kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="c4dbf-200">Aşağıdaki örnek, bir Active Directory kullanıcı olarak adlandırılır ve gösterir *TestUser* kendi etki alanı ile bir sertifika kullanılarak şifrelenmiş parola adlı *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="c4dbf-201">Kullanabileceğiniz `Invoke-ServiceFabricEncryptText` gizli şifreli metin oluşturmak için PowerShell komutu.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="c4dbf-202">Bkz: [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="c4dbf-203">Bir bant dışı yöntem kullanarak yerel makineye parolasının şifresi sertifikanın özel anahtarı dağıtmanız gerekir (Azure'da, Azure Resource Manager aracılığıyla budur).</span><span class="sxs-lookup"><span data-stu-id="c4dbf-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="c4dbf-204">Ardından, Service Fabric makineye hizmet paketini dağıtırken, gizli şifresini çözmek ve bu kimlik bilgileri altında çalıştırmak için Active Directory ile (kullanıcı adı ile birlikte) kimlik doğrulaması yapmak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="c4dbf-205">Grup yönetilen hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="c4dbf-206">Tek başına yükleyici kullanarak Windows sunucusuna yüklenen Service Fabric bir örneği için bir grup olarak yönetilen hizmet hesabı (gMSA) hizmeti çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-206">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="c4dbf-207">Bu Active Directory olduğuna dikkat edin, etki alanı içinde şirket içi ve Azure Active Directory (Azure AD) ile değil.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c4dbf-208">Bir gmsa'yı kullanarak bir parola olduğundan veya şifrelenmiş parola depolanır `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-208">By using a gMSA there is no password or encrypted password stored in the `Application Manifest`.</span></span>

<span data-ttu-id="c4dbf-209">Aşağıdaki örnek olarak adlandırılan bir gMSA hesabının nasıl oluşturulacağını gösterir *svc Test$*; Bu yönetilen hizmet hesabı küme düğümlerine; dağıtma ve kullanıcı asıl adı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-209">The following example shows how to create a gMSA account called *svc-Test$*; how to deploy that managed service account to the cluster nodes; and how to configure the user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="c4dbf-210">Önkoşullar.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-210">Prerequisites.</span></span>
- <span data-ttu-id="c4dbf-211">Etki alanı bir KDS kök anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-211">The domain needs a KDS root key.</span></span>
- <span data-ttu-id="c4dbf-212">Etki alanı bir Windows Server 2012 veya sonraki işlev düzeyinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-212">The domain needs to be at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="c4dbf-213">Örnek</span><span class="sxs-lookup"><span data-stu-id="c4dbf-213">Example</span></span>
1. <span data-ttu-id="c4dbf-214">Bir grup yönetilen hizmet hesabı kullanarak oluşturduğunuz active directory etki alanı yöneticisi olan `New-ADServiceAccount` komutunu ve emin `PrincipalsAllowedToRetrieveManagedPassword` service fabric küme düğümlerinin tümü içerir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-214">Have an active directory domain administrator create a group managed service account using the `New-ADServiceAccount` commandlet and ensure that the `PrincipalsAllowedToRetrieveManagedPassword` includes all of the service fabric cluster nodes.</span></span> <span data-ttu-id="c4dbf-215">Unutmayın `AccountName`, `DnsHostName`, ve `ServicePrincipalName` benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="c4dbf-216">Her service fabric küme düğümlerinin (örneğin, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`) yükleyin ve gMSA test.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-216">On each of the service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test the gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="c4dbf-217">Kullanıcı asıl adı yapılandırmak ve kullanıcı başvurmak için RunAsPolicy yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-217">Configure the User principal, and configure the RunAsPolicy to reference the user.</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="c4dbf-218">HTTP ve HTTPS uç noktaları için bir güvenlik erişim ilkesi atama</span><span class="sxs-lookup"><span data-stu-id="c4dbf-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="c4dbf-219">Bir hizmet için bir RunAs ilkesi uygulamak ve uç nokta kaynakları HTTP protokolü ile hizmet bildirimi bildirir, belirtmelisiniz bir **SecurityAccessPolicy** Bu uç noktaları için ayrılmış bağlantı noktaları doğru olduğundan emin olmak için Access-control hizmetinin altında çalıştığı RunAs kullanıcı hesabı için listelenen.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-219">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="c4dbf-220">Aksi takdirde, **http.sys** hizmetine erişiminiz yok ve istemciden çağrıları hatalarıyla alın.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-220">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="c4dbf-221">Aşağıdaki örnek, adlı bir uç nokta Customer1 hesabı uygular **EndpointName**, sağlayan, tam erişim hakları.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-221">The following example applies the Customer1 account to an endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="c4dbf-222">HTTPS uç noktası için aynı zamanda istemciye döndürmek için sertifikanın adı belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-222">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="c4dbf-223">Kullanarak bunu yapabilirsiniz **EndpointBindingPolicy**, uygulama bildirimi sertifikaları bölümünde tanımlanan sertifika ile.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-223">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="c4dbf-224">Https uç noktaları birden çok uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="c4dbf-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="c4dbf-225">Kullanmamaya dikkat etmeniz gereken **aynı bağlantı noktasını** http kullanırken aynı uygulamanın farklı örnekleri için**s**.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-225">You need to be careful not to use the **same port** for different instances of the same application when using http**s**.</span></span> <span data-ttu-id="c4dbf-226">Service Fabric uygulaması örneklerden birini için sertifika yükseltmeniz mümkün olmayacaktır nedenidir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-226">The reason is that Service Fabric won't be able to upgrade the cert for one of the application instances.</span></span> <span data-ttu-id="c4dbf-227">Örneğin, 1 veya uygulama 2 hem uygulaması kendi sertifikası 1 cert 2 yükseltmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-227">For example, if application 1 or application 2 both want to upgrade their cert 1 to cert 2.</span></span> <span data-ttu-id="c4dbf-228">Yükseltme gerçekleştiğinde, diğer uygulama hala kullanarak olsa bile Service Fabric sertifikası 1 kayıt http.sys ile yukarı temizlendi.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-228">When the upgrade happens, Service Fabric might have cleaned up the cert 1 registration with http.sys even though the other application is still using it.</span></span> <span data-ttu-id="c4dbf-229">Bunu önlemek için Service Fabric olmadığını zaten başka bir uygulama örneği bağlantı noktası (http.sys) nedeniyle sertifika ile kayıtlı ve işlem başarısız algılar.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-229">To prevent this, Service Fabric detects that there is already another application instance registered on the port with the certificate (due to http.sys) and fails the operation.</span></span>

<span data-ttu-id="c4dbf-230">Bu nedenle Service Fabric kullanan iki farklı hizmet yükseltmeyi desteklemez **aynı bağlantı noktasını** farklı uygulama durumlarda.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-230">Hence Service Fabric does not support upgrading two different services using **the same port** in different application instances.</span></span> <span data-ttu-id="c4dbf-231">Diğer bir deyişle, aynı bağlantı noktasında farklı Hizmetleri aynı sertifikayı kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-231">In other words, you cannot use the same certificate on different services on the same port.</span></span> <span data-ttu-id="c4dbf-232">Aynı bağlantı noktasında paylaşılan bir sertifikanız gerekiyorsa, hizmetleri yerleştirme kısıtlamalarına sahip farklı makinelerde yerleştirilir emin olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-232">If you need to have a shared certificate on the same port, you need to ensure that the services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="c4dbf-233">Veya her uygulama örneği her hizmet için Service Fabric dinamik bağlantı noktaları mümkünse kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="c4dbf-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="c4dbf-234">Https, "Windows HTTP sunucu API birden çok sertifika bir bağlantı noktasını paylaşmak uygulamalar için desteklemiyor." bildiren uyarı bir hata ile yükseltme bir hata görürseniz</span><span class="sxs-lookup"><span data-stu-id="c4dbf-234">If you see an upgrade fail with https, an error warning saying "The Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="c4dbf-235">Tam uygulama bildirim örneği</span><span class="sxs-lookup"><span data-stu-id="c4dbf-235">A complete application manifest example</span></span>
<span data-ttu-id="c4dbf-236">Aşağıdaki uygulama bildirimi birçok farklı ayarı gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4dbf-236">The following application manifest shows many of the different settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="c4dbf-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4dbf-237">Next steps</span></span>
* [<span data-ttu-id="c4dbf-238">Uygulama modeli anlama</span><span class="sxs-lookup"><span data-stu-id="c4dbf-238">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="c4dbf-239">Bir hizmet bildirimi kaynakları belirtme</span><span class="sxs-lookup"><span data-stu-id="c4dbf-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="c4dbf-240">Bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="c4dbf-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
