---
title: "Azure mikro güvenlik ilkeleri hakkında aaaLearn | Microsoft Docs"
description: "Başlamadan önce nasıl eylem burada bir uygulamanın tooperform bazı ihtiyacı hello SetupEntry noktası dahil toorun sistem ve yerel güvenlik hesapları altından bir Service Fabric uygulaması, ayrıcalıklı bir genel bakış"
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
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="6650a-103">Uygulamanıza yönelik güvenlik ilkeleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6650a-103">Configure security policies for your application</span></span>
<span data-ttu-id="6650a-104">Azure Service Fabric kullanarak hello kümedeki farklı kullanıcı hesabı altında çalışan uygulamaları güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="6650a-105">Service Fabric ayrıca uygulamalar tarafından hello kullanıcı hesapları altında--dağıtımının hello zamanında örneğin kullanılan güvenli hello kaynakları, dizinleri ve dosyaları sertifikaları yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6650a-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="6650a-106">Bu çalışan uygulamaları bile paylaşılan bir barındırılan ortamda, diğerinden daha güvenli hale getirir.</span><span class="sxs-lookup"><span data-stu-id="6650a-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="6650a-107">Varsayılan olarak, Service Fabric uygulamaları hello Fabric.exe işlemin altında çalıştığı hello hesap altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="6650a-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="6650a-108">Service Fabric, aynı zamanda bir yerel kullanıcı hesabı veya hello uygulama bildirimi içinde belirtilen yerel sistem hesabı altında toorun uygulamaları hello yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="6650a-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="6650a-109">Desteklenen yerel sistem hesabı türleri **YerelKullanıcı**, **NetworkService**, **Yerelhizmet**, ve **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="6650a-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="6650a-110">Merhaba tek başına yükleyici kullanarak, veri merkezinizde Windows Server'da Service Fabric çalıştırıyorsanız, Grup yönetilen hizmet hesapları dahil olmak üzere Active Directory etki alanı hesaplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="6650a-111">Tanımlayabilir ve kullanıcı grupları oluşturun, böylece bir veya daha fazla kullanıcı birlikte yönetilen tooeach Grup toobe eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6650a-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="6650a-112">Bu, farklı hizmet giriş noktaları için birden çok kullanıcı ve bunlar toohave hello grup düzeyinde kullanılabilen ortak belirli ayrıcalıklara gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="6650a-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="6650a-113">Bir hizmet Kurulum giriş noktası için Hello ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6650a-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="6650a-114">Hello açıklandığı gibi [uygulama modeli](service-fabric-application-model.md), hello Kurulum giriş noktası **SetupEntryPoint**, hello Service Fabric aynı kimlik bilgileri ile çalışan bir ayrıcalıklı giriş noktasıdır (genellikle hello *NetworkService* hesabı) önce başka bir giriş noktası.</span><span class="sxs-lookup"><span data-stu-id="6650a-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="6650a-115">tarafından belirtilen hello yürütülebilir **EntryPoint** genellikle hello uzun süre çalışan hizmet ana bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="6650a-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="6650a-116">Bu nedenle ayrı Kurulum giriş noktası sahip uzun süre için toorun hello hizmet konağı yüksek ayrıcalıklara sahip yürütülebilir belirlemeyi önler.</span><span class="sxs-lookup"><span data-stu-id="6650a-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="6650a-117">Merhaba yürütülebilir, **EntryPoint** belirtir çalıştırıldıktan **SetupEntryPoint** başarıyla çıkar.</span><span class="sxs-lookup"><span data-stu-id="6650a-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="6650a-118">Merhaba elde edilen işlem izlenen ve yeniden ve yeniden ile başlayan **SetupEntryPoint** hiç sonlandırır veya çöküyor.</span><span class="sxs-lookup"><span data-stu-id="6650a-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="6650a-119">Merhaba aşağıda gösterildiği SetupEntryPoint hello ve hello hizmeti için ana EntryPoint hello bir basit hizmeti bildirim örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6650a-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

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

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="6650a-120">Yerel bir hesap kullanarak Hello ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6650a-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="6650a-121">Merhaba hizmet toohave Kurulum giriş noktası yapılandırdıktan sonra hello uygulama bildiriminde altında çalıştığı hello güvenlik izinlerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="6650a-122">Aşağıdaki örneğine hello nasıl tooconfigure hello hizmet toorun kullanıcı yönetici hesabının ayrıcalıklarını altında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="6650a-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

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

<span data-ttu-id="6650a-123">İlk olarak, oluşturma bir **sorumluları** SetupAdminUser gibi bir kullanıcı adı bölümü.</span><span class="sxs-lookup"><span data-stu-id="6650a-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="6650a-124">Bu hello kullanıcı hello yöneticiler sistem grubunun bir üyesi olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="6650a-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="6650a-125">Sonraki hello altında **ServiceManifestImport** bölümünde, bir ilke tooapply bu asıl çok yapılandırmak**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="6650a-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="6650a-126">Bu Service Fabric, hello zaman söyler **MySetup.bat** dosyasını çalıştırın, olmalıdır `RunAs` yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="6650a-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="6650a-127">Sahip olduğunuz o *değil* uygulanan bir ilke toohello ana giriş noktası, hello kodda **MyServiceHost.exe** hello sisteminde çalışıyor **NetworkService** hesabı.</span><span class="sxs-lookup"><span data-stu-id="6650a-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="6650a-128">Bu, tüm hizmet giriş noktaları olarak çalıştırılan hello varsayılan hesaptır.</span><span class="sxs-lookup"><span data-stu-id="6650a-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="6650a-129">Şimdi hello dosya MySetup.bat toohello Visual Studio Proje tootest hello yönetici ayrıcalıkları ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="6650a-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="6650a-130">Visual Studio'da hello hizmeti projesine sağ tıklayın ve MySetup.bat adlı yeni bir dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6650a-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="6650a-131">Ardından, o hello MySetup.bat dosya hello hizmet paketinde bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6650a-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="6650a-132">Varsayılan olarak, bu değil.</span><span class="sxs-lookup"><span data-stu-id="6650a-132">By default, it is not.</span></span> <span data-ttu-id="6650a-133">Hello dosya seçin, tooget hello bağlam menüsü sağ tıklayın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="6650a-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="6650a-134">Merhaba Özellikleri iletişim kutusunda emin **tooOutput dizin kopyalama** çok ayarlanır**yeniyse Kopyala**.</span><span class="sxs-lookup"><span data-stu-id="6650a-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="6650a-135">Aşağıdaki ekran görüntüsü hello bakın.</span><span class="sxs-lookup"><span data-stu-id="6650a-135">See hello following screenshot.</span></span>

![SetupEntryPoint toplu iş dosyası için Visual Studio CopyToOutput][image1]

<span data-ttu-id="6650a-137">Şimdi hello MySetup.bat dosyasını açın ve aşağıdaki komutları hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6650a-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="6650a-138">Ardından, yapı ve hello çözüm tooa yerel geliştirme kümesi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="6650a-139">Service Fabric Explorer'da gösterildiği gibi Hello hizmeti başlatıldıktan sonra bu hello MySetup.bat dosyasını iki yolla başarılı olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="6650a-140">Bir PowerShell komut istemi açıp türü:</span><span class="sxs-lookup"><span data-stu-id="6650a-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="6650a-141">Ardından, burada hello hizmet dağıtıldı ve Service Fabric Explorer'da--Örneğin, düğüm 2 başlatılan hello düğümü hello adını not edin.</span><span class="sxs-lookup"><span data-stu-id="6650a-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="6650a-142">Ardından, hello değerini gösteren toohello uygulama örneği çalışma klasörü toofind hello out.txt dosyasını gidin **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="6650a-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="6650a-143">Bu hizmet dağıtılan tooNode 2 olduysa, örneğin, daha sonra hello toothis yolu geçebilir **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="6650a-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="6650a-144">Yerel Sistem hesapları kullanarak Hello ilkesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6650a-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="6650a-145">Genellikle, bir yönetici hesabı yerine yerel sistem hesabı kullanarak tercih toorun hello başlangıç komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="6650a-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="6650a-146">Yöneticiler grubunun da makineler kullanıcı erişim denetimi (UAC) varsayılan olarak etkin olduğundan genellikle işe yaramazsa hello üyesi olarak Hello RunAs İlkesi çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="6650a-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="6650a-147">Böyle durumlarda, **hello önerilir toorun hello LocalSystem olarak SetupEntryPoint yerine yerel kullanıcı eklenen tooAdministrators grup olarak**.</span><span class="sxs-lookup"><span data-stu-id="6650a-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="6650a-148">Merhaba aşağıdaki örnekte ayarı hello SetupEntryPoint toorun LocalSystem olarak gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6650a-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="6650a-149">PowerShell komutlarını bir Kurulum giriş noktasından Başlat</span><span class="sxs-lookup"><span data-stu-id="6650a-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="6650a-150">Merhaba gelen PowerShell toorun **SetupEntryPoint** noktası çalıştırabilirsiniz **PowerShell.exe** tooa PowerShell işaret eden bir toplu iş dosyasında dosya.</span><span class="sxs-lookup"><span data-stu-id="6650a-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="6650a-151">İlk olarak, PowerShell dosya toohello hizmet projesi--Örneğin, ekleyin **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="6650a-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="6650a-152">Tooset hello unutmayın *yeniyse Kopyala* hello dosyayı ayrıca hello hizmet paketine dahil şekilde özelliği.</span><span class="sxs-lookup"><span data-stu-id="6650a-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="6650a-153">Merhaba aşağıdaki örnek olarak adlandırılan bir sistem ortam değişkenini ayarlar MySetup.ps1 adlı bir PowerShell dosya başlayan bir örnek toplu iş dosyası gösterir **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="6650a-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="6650a-154">MySetup.bat toostart PowerShell dosyası:</span><span class="sxs-lookup"><span data-stu-id="6650a-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="6650a-155">Merhaba PowerShell dosyasında tooset bir sistem ortam değişkeni aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6650a-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="6650a-156">Merhaba toplu iş dosyası çalıştığında, varsayılan olarak, hello uygulama klasörü adlı görünüyor **iş** dosyaları için.</span><span class="sxs-lookup"><span data-stu-id="6650a-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="6650a-157">MySetup.bat çalıştığında, bu durumda, bu toofind hello MySetup.ps1 dosya hello aynı istiyoruz hello uygulama klasörü **kod paketi** klasör.</span><span class="sxs-lookup"><span data-stu-id="6650a-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="6650a-158">toochange bu klasör, kümesi hello çalışma klasörü:</span><span class="sxs-lookup"><span data-stu-id="6650a-158">toochange this folder, set hello working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="6650a-159">Yerel hata ayıklama için konsolu yeniden yönlendirmeyi kullanma</span><span class="sxs-lookup"><span data-stu-id="6650a-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="6650a-160">Bazen, yararlı toosee hello konsol çıkışı'hata ayıklama amacıyla bir komut dosyası çalıştırılarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="6650a-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="6650a-161">toodo bunu hello çıkış tooa dosyasını yazar konsol yeniden yönlendirme ilkesi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="6650a-162">Merhaba yazılı toohello uygulama klasörü adlı çıkış dosyası **günlük** burada hello uygulamanın dağıtıldığı ve Çalıştır hello düğümde.</span><span class="sxs-lookup"><span data-stu-id="6650a-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="6650a-163">(Where bkz toofind Bu örnek önceki hello.)</span><span class="sxs-lookup"><span data-stu-id="6650a-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="6650a-164">Hiçbir zaman bu hello uygulama yük devretme etkileyebileceğinden üretimde dağıtılan bir uygulamada hello konsol yeniden yönlendirme ilkesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6650a-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="6650a-165">*Yalnızca* bunu yerel geliştirme ve hata ayıklama amacıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="6650a-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="6650a-166">Merhaba aşağıdaki örnek ayarı hello konsol yeniden yönlendirmesi FileRetentionCount değeriyle gösterir:</span><span class="sxs-lookup"><span data-stu-id="6650a-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="6650a-167">Merhaba MySetup.ps1 dosya toowrite şimdi değiştirirseniz bir **Echo** komutu, bu hata ayıklama amacıyla toohello çıktı dosyasına yazma:</span><span class="sxs-lookup"><span data-stu-id="6650a-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="6650a-168">**Bu konsol yeniden yönlendirme ilkesi, komut dosyası hata ayıklama sonra hemen kaldırın**.</span><span class="sxs-lookup"><span data-stu-id="6650a-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="6650a-169">Hizmet kodu paketleri için bir ilke yapılandırın</span><span class="sxs-lookup"><span data-stu-id="6650a-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="6650a-170">Önceki adımları hello gördüğünüz nasıl tooapply RunAs İlkesi tooSetupEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="6650a-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="6650a-171">Olarak uygulanan toocreate farklı ilkeleri ilkeler nasıl hizmet uygulamasına biraz daha derin bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="6650a-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="6650a-172">Yerel kullanıcı grupları oluşturun</span><span class="sxs-lookup"><span data-stu-id="6650a-172">Create local user groups</span></span>
<span data-ttu-id="6650a-173">Tanımlamak ve bir izin kullanıcı grupları oluşturun veya daha fazla kullanıcı toobe tooa Grup eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="6650a-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="6650a-174">Bu, birden çok kullanıcı için farklı hizmet giriş noktaları vardır ve bunlar toohave hello grup düzeyinde kullanılabilen bazı ortak ayrıcalıklarına sahip olmanız gerekir yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="6650a-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="6650a-175">Merhaba aşağıdaki örnekte gösterilir adlı bir yerel grup **LocalAdminGroup** yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="6650a-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="6650a-176">İki kullanıcılar, Customer1 ve Customer2, bu yerel grubun üyesi yapılır.</span><span class="sxs-lookup"><span data-stu-id="6650a-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="6650a-177">Yerel kullanıcılar oluşturma</span><span class="sxs-lookup"><span data-stu-id="6650a-177">Create local users</span></span>
<span data-ttu-id="6650a-178">Bir hizmet Merhaba uygulaması içinde kullanılan toohelp güvenli olabilir yerel bir kullanıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="6650a-179">Zaman bir **YerelKullanıcı** hesap türü belirtilen hello ilkeleri bölümünde hello uygulama bildiriminin, Service Fabric hello uygulamanın dağıtıldığı makinelerde yerel kullanıcı hesaplarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6650a-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="6650a-180">Varsayılan olarak, bu hesapları (örneğin, aşağıdaki örnek hello Customer3) hello uygulamada belirtilenlerle aynı adları bildirim hello sahip değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="6650a-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="6650a-181">Bunun yerine, dinamik olarak oluşturulur ve rastgele parolalara sahip.</span><span class="sxs-lookup"><span data-stu-id="6650a-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="6650a-182">Bir uygulama hello kullanıcı hesabı ve parolası (örneğin, tooenable NTLM kimlik doğrulaması) tüm makinelerde aynı olmasını gerektirir, hello küme bildiriminde NTLMAuthenticationEnabled tootrue ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6650a-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="6650a-183">Merhaba küme bildirimi de kullanılan bir NTLMAuthenticationPasswordSecret belirtmelisiniz toogenerate tüm makinelerde aynı parola hello.</span><span class="sxs-lookup"><span data-stu-id="6650a-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="6650a-184">Hizmet kodu paketleri ilkeleri toohello atayın</span><span class="sxs-lookup"><span data-stu-id="6650a-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="6650a-185">Merhaba **RunAsPolicy** bölümünde bir **ServiceManifestImport** kullanılan toorun kod paketi olmalıdır hello sorumluları bölümünden hello hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6650a-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="6650a-186">Ayrıca hello ilkeleri bölümünde kullanıcı hesaplarıyla hello hizmet paketlerinden bildirim kodu ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="6650a-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="6650a-187">Bu hello Kurulum veya ana giriş noktaları için belirtebilirsiniz veya belirtebilirsiniz `All` tooapply, tooboth.</span><span class="sxs-lookup"><span data-stu-id="6650a-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="6650a-188">Merhaba aşağıdaki örnek uygulanan farklı ilkeleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="6650a-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="6650a-189">Varsa **EntryPointType** belirtilmezse, hello varsayılan tooEntryPointType Ayarla "Ana" =.</span><span class="sxs-lookup"><span data-stu-id="6650a-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="6650a-190">Belirtme **SetupEntryPoint** belirli yüksek ayrıcalıklı kurulum işlemlerini sistem hesabı altında toorun istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="6650a-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="6650a-191">Merhaba gerçek hizmet kodu düşük ayrıcalıklı hesap altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="6650a-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="6650a-192">Bir varsayılan ilke tooall hizmet kod paketleri Uygula</span><span class="sxs-lookup"><span data-stu-id="6650a-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="6650a-193">Merhaba kullandığınız **DefaultRunAsPolicy** bölüm toospecify belirli bir sahip olmayan tüm kod paketler için varsayılan bir kullanıcı hesabı **RunAsPolicy** tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="6650a-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="6650a-194">Bir uygulama tarafından kullanılan hello hizmet bildiriminde belirtilen hello kod paketleri çoğunu toorun altında gerekiyorsa aynı kullanıcı hello hello uygulama yalnızca, kullanıcı hesabı ile varsayılan bir RunAs ilke tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6650a-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="6650a-195">kod paketi yoksa hello aşağıdaki örnek belirleyen bir **RunAsPolicy** belirtilen hello kod paketi hello altında çalışması gerektiğini **MyDefaultAccount** hello ilkeleri bölümünde belirtilen.</span><span class="sxs-lookup"><span data-stu-id="6650a-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="6650a-196">Bir Active Directory etki alanı grubu veya kullanıcı kullanın</span><span class="sxs-lookup"><span data-stu-id="6650a-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="6650a-197">Merhaba tek başına yükleyici kullanarak Windows sunucusuna yüklenen Service Fabric bir örneği için Active Directory kullanıcı veya grup hesabına ait hello hizmeti hello kimlik bilgileri altında çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="6650a-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="6650a-198">Bu içi etki alanınızda Active Directory ve Azure Active Directory (Azure AD) değil.</span><span class="sxs-lookup"><span data-stu-id="6650a-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6650a-199">Bir etki alanı kullanıcısı veya grubu kullanarak (örneğin, dosya paylaşımları) hello etki alanındaki izinleri verilmiş diğer kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="6650a-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="6650a-200">Merhaba aşağıdaki örnekte gösterilir adlı bir Active Directory kullanıcı *TestUser* kendi etki alanı ile bir sertifika kullanılarak şifrelenmiş parola adlı *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="6650a-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="6650a-201">Merhaba kullanabilirsiniz `Invoke-ServiceFabricEncryptText` PowerShell komut toocreate hello gizli şifreli metin.</span><span class="sxs-lookup"><span data-stu-id="6650a-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="6650a-202">Bkz: [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6650a-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="6650a-203">Bir bant dışı yöntem kullanarak özel anahtarı hello sertifika toodecrypt hello parola toohello yerel makine hello dağıtmanız gerekir (Azure'da, Azure Resource Manager aracılığıyla budur).</span><span class="sxs-lookup"><span data-stu-id="6650a-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="6650a-204">Ardından, Service Fabric hello hizmet paketi toohello makine dağıtırken mümkün toodecrypt hello parolası ve (Merhaba kullanıcı adı ile birlikte) bu kimlik bilgileri altında Active Directory toorun ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="6650a-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="6650a-205">Grup yönetilen hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="6650a-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="6650a-206">Merhaba tek başına yükleyici kullanarak Windows sunucusuna yüklenen Service Fabric bir örneği için bir grup olarak yönetilen hizmet hesabı (gMSA) hello hizmeti çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="6650a-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="6650a-207">Bu Active Directory olduğuna dikkat edin, etki alanı içinde şirket içi ve Azure Active Directory (Azure AD) ile değil.</span><span class="sxs-lookup"><span data-stu-id="6650a-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6650a-208">Bir gmsa'yı kullanarak parola veya yoktur hello depolanan şifrelenmiş parola `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="6650a-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="6650a-209">Merhaba aşağıdaki örnekte nasıl toocreate gMSA hesabı olarak adlandırılan gösterir *svc Test$*; toodeploy yönetilen nasıl hizmet hesabı toohello küme düğümleri; ve nasıl tooconfigure hello kullanıcı asıl adı.</span><span class="sxs-lookup"><span data-stu-id="6650a-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="6650a-210">Önkoşullar.</span><span class="sxs-lookup"><span data-stu-id="6650a-210">Prerequisites.</span></span>
- <span data-ttu-id="6650a-211">Merhaba etki alanı bir KDS kök anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6650a-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="6650a-212">Windows Server 2012 veya sonraki işlev düzeyinde toobe Hello etki alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6650a-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="6650a-213">Örnek</span><span class="sxs-lookup"><span data-stu-id="6650a-213">Example</span></span>
1. <span data-ttu-id="6650a-214">Hello kullanarak Grup yönetilen hizmet hesabı oluşturma bir active directory etki alanı yöneticisi olan `New-ADServiceAccount` komutunu ve o hello olun `PrincipalsAllowedToRetrieveManagedPassword` hello service fabric küme düğümlerinin tümü içerir.</span><span class="sxs-lookup"><span data-stu-id="6650a-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="6650a-215">Unutmayın `AccountName`, `DnsHostName`, ve `ServicePrincipalName` benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6650a-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="6650a-216">Her hello service fabric küme düğümlerinin (örneğin, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`) yükleyin ve hello gMSA sınayın.</span><span class="sxs-lookup"><span data-stu-id="6650a-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="6650a-217">Merhaba kullanıcı asıl yapılandırmak ve hello RunAsPolicy tooreference hello kullanıcı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="6650a-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="6650a-218">HTTP ve HTTPS uç noktaları için bir güvenlik erişim ilkesi atama</span><span class="sxs-lookup"><span data-stu-id="6650a-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="6650a-219">Bir RunAs İlkesi tooa hizmeti uygulamak ve hello hizmet bildirimi uç noktası kaynakları hello HTTP protokolü ile bildirir, belirtmelisiniz bir **SecurityAccessPolicy** tooensure bağlantı noktalarını toothese uç noktaları ayrılmış olan doğru erişim denetimi için hello hello hizmetinin altında çalıştığı RunAs kullanıcı hesabı listelenir.</span><span class="sxs-lookup"><span data-stu-id="6650a-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="6650a-220">Aksi takdirde, **http.sys** erişim toohello hizmeti gerekmemesi ve hello istemciden çağrıları hatalarıyla alın.</span><span class="sxs-lookup"><span data-stu-id="6650a-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="6650a-221">Merhaba aşağıdaki örnek uygular hello Customer1 hesap tooan uç nokta adı verilen **EndpointName**, sağlayan, tam erişim hakları.</span><span class="sxs-lookup"><span data-stu-id="6650a-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="6650a-222">Merhaba HTTPS uç noktası için aynı zamanda hello sertifika tooreturn toohello istemcisi tooindicate hello adına sahip.</span><span class="sxs-lookup"><span data-stu-id="6650a-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="6650a-223">Kullanarak bunu yapabilirsiniz **EndpointBindingPolicy**, hello uygulama bildirimi sertifikaları bölümünde tanımlanan hello sertifikayla.</span><span class="sxs-lookup"><span data-stu-id="6650a-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="6650a-224">Https uç noktaları birden çok uygulama yükseltme</span><span class="sxs-lookup"><span data-stu-id="6650a-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="6650a-225">Toobe dikkatli ihtiyacınız olmayan toouse hello **aynı bağlantı noktasını** hello farklı örnekleri için http kullanırken aynı uygulama**s**.</span><span class="sxs-lookup"><span data-stu-id="6650a-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="6650a-226">Merhaba Service Fabric hello uygulama örnekleri biri için mümkün tooupgrade hello sertifika olmayacaktır nedenidir.</span><span class="sxs-lookup"><span data-stu-id="6650a-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="6650a-227">Örneğin, 1 veya uygulama 2 her iki uygulamanın kendi sertifikası 1 toocert 2 tooupgrade istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6650a-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="6650a-228">Merhaba yükseltme gerçekleştiğinde hello diğer uygulama hala bu kullanıyor olsa da Service Fabric http.sys hello sertifikası 1 kaydı yukarı temizlendi.</span><span class="sxs-lookup"><span data-stu-id="6650a-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="6650a-229">tooprevent Bu, Service Fabric algılar zaten var olduğu hello sertifikasıyla hello noktasında kayıtlı başka bir uygulama örneği (son toohttp.sys) ve hello işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="6650a-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="6650a-230">Bu nedenle Service Fabric kullanan iki farklı hizmet yükseltmeyi desteklemez **hello aynı bağlantı noktasını** farklı uygulama durumlarda.</span><span class="sxs-lookup"><span data-stu-id="6650a-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="6650a-231">Diğer bir deyişle, hello farklı Services'de üzerinde aynı sertifika hello kullanamazsınız aynı bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="6650a-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="6650a-232">Toohave gerekiyorsa paylaşılan sertifika hello üzerinde aynı bağlantı noktası, hizmetleri yerleştirme kısıtlamalarına sahip farklı makinelerde yerleştirilir bu hello tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="6650a-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="6650a-233">Veya her uygulama örneği her hizmet için Service Fabric dinamik bağlantı noktaları mümkünse kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="6650a-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="6650a-234">Https ile yükseltme bir hata görürseniz "Merhaba Windows HTTP Sunucusu API desteği yok birden çok sertifika bir bağlantı noktasını paylaşmak uygulamalar için." bildiren bir hata uyarısı</span><span class="sxs-lookup"><span data-stu-id="6650a-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="6650a-235">Tam uygulama bildirim örneği</span><span class="sxs-lookup"><span data-stu-id="6650a-235">A complete application manifest example</span></span>
<span data-ttu-id="6650a-236">uygulama bildirimini izleyerek hello hello birçoğu farklı ayarları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6650a-236">hello following application manifest shows many of hello different settings:</span></span>

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
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


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6650a-237">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6650a-237">Next steps</span></span>
* [<span data-ttu-id="6650a-238">Merhaba uygulama modelini anlama</span><span class="sxs-lookup"><span data-stu-id="6650a-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="6650a-239">Bir hizmet bildirimi kaynakları belirtme</span><span class="sxs-lookup"><span data-stu-id="6650a-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="6650a-240">Bir uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="6650a-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
