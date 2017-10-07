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
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Nasıl tooconfigure ve çalıştırma başlangıç için bir bulut hizmeti görevleri
Bir rolü başlamadan önce başlangıç görevleri tooperform işlemleri kullanabilirsiniz. Bir bileşeni yüklemek, COM bileşenlerini kaydetme, kayıt defteri anahtarlarını ayarlamak veya uzun süre çalışan bir işlem başlatılıyor tooperform isteyebilirsiniz işlemleri içerir.

> [!NOTE]
> Başlangıç değil yalnızca tooCloud Service Web ve çalışan rolleri geçerli tooVirtual makineleri görevlerdir.
> 
> 

## <a name="how-startup-tasks-work"></a>Başlangıç görevi nasıl çalışır
Başlangıç görevlerdir rollerinizi başlar ve hello tanımlanan önce gerçekleştirilen eylemler [ServiceDefinition.csdef] hello kullanarak dosya [görev] hello öğesinde [başlangıç]öğesi. Sık başlangıç görevleri toplu dosyalar, ancak bunlar aynı zamanda konsol uygulamaları veya PowerShell komut dosyalarını Başlat toplu iş dosyaları olabilir.

Ortam değişkenleri, bir başlangıç görevi bilgi aktarmak ve yerel depolama bir başlangıç görevi dışında kullanılan toopass bilgi olabilir. Örneğin, bir ortam değişkeni hello yolu tooa program belirtebilirsiniz tooinstall istediğiniz ve ardından daha sonra rolleri tarafından okunabilir toolocal depolama dosyaları yazılabilir.

Başlangıç görevi bilgileri ve hello tarafından belirtilen hataları toohello dizin oturum **TEMP** ortam değişkeni. Merhaba başlangıç görevi sırasında hello **TEMP** ortam değişkenini çözümler toohello *C:\\kaynakları\\temp\\[GUID]. [ Rol adı]\\RoleTemp* hello bulut üzerinde çalışırken dizin.

Başlangıç görevi yeniden başlatmalar arasında da birkaç kez çalıştırılabilir. Örneğin, hello başlangıç görevi hello rol geri dönüştürme her zaman çalıştırılır ve rol dönüştürür her zaman yeniden başlatma içermeyebilir. Başlangıç görevi sorunsuz birkaç kez toorun tanır şekilde yazılmalıdır.

Başlangıç görevleri ile bitmelidir bir **errorlevel** (veya çıkış kodu) hello başlatma işlemi toocomplete sıfır. Bir başlangıç görevi bir sıfır ile bitip bitmediğini **errorlevel**, hello rol başlatılmayacak.

## <a name="role-startup-order"></a>Rol başlatma sırası
Aşağıdaki listeler hello rol başlatma yordamı azure'da hello:

1. Merhaba örneği olarak işaretli **başlangıç** ve trafik almaz.
2. Tüm başlangıç görevleri tootheir göre yürütülür **taskType** özniteliği.
   
   * Merhaba **basit** görevler eşzamanlı olarak, yürütülen bir kerede.
   * Merhaba **arka plan** ve **ön plan** zaman uyumsuz olarak başlatılan, paralel toohello başlangıç görevi görevlerdir.  
     
     > [!WARNING]
     > Role özgü verileri kullanılabilir olmaması IIS tam olarak hello başlatma işleminde hello başlangıç görevi aşaması sırasında yapılandırılmamış olabilir. Role özgü veri gerektiren başlangıç görevleri kullanması gereken [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. Hello rol ana bilgisayar işlemi başlatıldı ve hello sitesi IIS içinde oluşturulur.
4. Merhaba [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) yöntemi çağrılır.
5. Merhaba örneği olarak işaretli **hazır** ve trafik yönlendirilmiş toohello örneği.
6. Merhaba [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi çağrılır.

## <a name="example-of-a-startup-task"></a>Bir başlangıç görevi örneği
Başlangıç görevi hello tanımlanmış [ServiceDefinition.csdef] dosyasında hello **görev** öğesi. Merhaba **commandLine** özniteliği hello adını belirtir ve hello başlangıç toplu parametrelerinin dosya veya komut, hello konsol **executionContext** özniteliği belirtir hello başlangıç hello ayrıcalık düzeyi Görev ve hello **taskType** özniteliği belirtir nasıl hello görev yürütülür.

Bu örnekte, bir ortam değişkeni **MyVersionNumber**, hello başlangıç görevi için oluşturulan ve toohello değerini "**1.0.0.0**".

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

Aşağıdaki örneğine hello hello **Startup.cmd** toplu iş dosyası hello TEMP ortam değişkeni tarafından belirtilen hello dizininde "Merhaba geçerli sürüm 1.0.0.0" toohello StartupLog.txt dosyası hello satır yazar. Merhaba `EXIT /B 0` satır sağlar, hello başlangıç görevi sonlandırır ile bir **errorlevel** sıfır.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> Visual Studio'da hello **tooOutput dizin kopyalama** özelliği başlangıç toplu işlem dosyanız için çok ayarlanmalıdır**her zaman Kopyala** toobe başlangıç toplu iş dosyası doğru olduğundan emin dağıtılan Azure tooyour projede (**approot\\bin** Web rolleri için ve **approot** çalışan roller için).
> 
> 

## <a name="description-of-task-attributes"></a>Görev öznitelikler açıklaması
Merhaba aşağıdaki hello özniteliklerini hello açıklayan **görev** hello öğesinde [ServiceDefinition.csdef] dosyası:

**komut satırı** -hello başlangıç görevi için hello komut satırını belirtir:

* Merhaba başlangıç görevi başlatan hello komutuyla, isteğe bağlı komut satırı parametreleri.
* Sık hello filename .cmd veya .bat toplu iş dosyası budur.
* Merhaba görevdir göreli toohello AppRoot\\Bin klasörü hello dağıtımı için. Ortam değişkenleri hello yolu ve dosya hello görevinin belirlerken genişletilir değil. Ortam genişletme gerekiyorsa, başlangıç görevi çağıran bir küçük .cmd komut dosyası oluşturabilirsiniz.
* Bir konsol uygulaması ya da başlayan bir toplu iş dosyası bir [PowerShell Betiği](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -hello başlangıç görevi hello ayrıcalık düzeyini belirtir. Merhaba ayrıcalık düzeyi sınırlı veya yükseltilmiş:

* **sınırlı**  
  aynı hello rolü olarak ayrıcalıkları hello ile Merhaba başlangıç görevi çalıştırır. Ne zaman hello **executionContext** özniteliği hello için [çalışma zamanı] öğesidir de **sınırlı**, kullanıcı ayrıcalıkları kullanılır.
* **yükseltilmiş**  
  Merhaba başlangıç görevi yönetici ayrıcalıklarıyla çalıştırır. Bu başlangıç görevleri tooinstall programları sağlar, IIS yapılandırma değişiklikleri, hello ayrıcalık düzeyi hello rolünün kendisini artırmadan kayıt defteri değişikliklerini ve diğer yönetici düzeyi görevleri gerçekleştirmek.  

> [!NOTE]
> Merhaba ayrıcalık düzeyi başlangıç görevinin ihtiyaç duymadığı toobe hello aynı hello rolü olarak kendisi.
> 
> 

**taskType** -hello şekilde bir başlangıç görevi yürütüldüğünde belirtir.

* **Basit**  
  Görevlerin yürütülme eşzamanlı olarak, bir kerede, hello sırayla hello belirtilen [ServiceDefinition.csdef] dosya. Bir zaman **basit** başlangıç görevi sonlandırır ile bir **errorlevel** hiç biri, sonraki hello **basit** başlangıç görevi gerçekleştirilir. Artık böyle olduğunda **basit** başlangıç görevleri tooexecute, sonra da hello rol kendisi başlatılır.   
  
  > [!NOTE]
  > Merhaba, **basit** görev bir sıfır ile biten **errorlevel**, hello örneği engellenir. Sonraki **basit** başlangıç görevleri ve hello rol kendisinin başlatılmayacak.
  > 
  > 
  
    Toplu iş dosyası ile biten tooensure bir **errorlevel** hiç biri hello bağlamını `EXIT /B 0` toplu iş dosyası işleminizi hello sonunda.
* **arka plan**  
  Görevler hello başlangıç hello rolünün ile paralel zaman uyumsuz olarak çalıştırılır.
* **ön plan**  
  Görevler hello başlangıç hello rolünün ile paralel zaman uyumsuz olarak çalıştırılır. Merhaba arasındaki temel farklılık bir **ön plan** ve **arka plan** görev olan bir **ön plan** görev engeller hello rol geri dönüştürme veya hello görev olana kadar kapatılıyor sona erdi. Merhaba **arka plan** görevleri bu kısıtlama yok.

## <a name="environment-variables"></a>Ortam değişkenleri
Ortam değişkenleri bir şekilde toopass bilgi tooa başlangıç görevi kullanılabilir. Örneğin, bir program tooinstall içeren hello yolu tooa blob veya rolünüze kullanacağı bağlantı noktası numaralarını veya ayarları toocontrol özellikleri, başlangıç görevinin koyabilirsiniz.

Başlangıç görevler için ortam değişkenleri iki tür vardır; statik ortam değişkenleri ve ortam değişkenleri göre hello üyelerinde [ RoleEnvironment] sınıfı. Her ikisi de hello olan [ortam] hello bölümünü [ServiceDefinition.csdef] dosya ve her iki kullanım hello [değişken] öğesi ve **adı** özniteliği.

Statik ortam değişkenlerini kullanır hello **değeri** hello özniteliği [değişken] öğesi. Yukarıdaki Hello örneği oluşturur hello ortam değişkeni **MyVersionNumber** statik değeri olan "**1.0.0.0**". Başka bir örnek toocreate olabilir bir **StagingOrProduction** toovalues, el ile ayarlayabilirsiniz ortam değişkeni "**hazırlama**"veya"**üretim**" tooperform farklı bir başlangıç Eylemler dayalı hello hello değerini **StagingOrProduction** ortam değişkeni.

Ortam değişkenleri hello RoleEnvironment sınıfı üyelerinde dayalı hello kullanmayın **değeri** hello özniteliği [değişken] öğesi. Bunun yerine, hello [RoleInstanceValue] hello uygun olan alt öğesi **XPath** öznitelik değeri, belirli bir hello üyede dayalı bir ortam değişkeni kullanılan toocreate olan [ RoleEnvironment] sınıfı. Merhaba değerlerini **XPath** tooaccess çeşitli öznitelik [ RoleEnvironment] değerler bulunabilir [burada](cloud-services-role-config-xpath.md).

Örneğin, toocreate olan bir ortam değişkeni "**true**" Merhaba örneği hello işlem öykünücüsünde çalıştırırken ve "**false**" Merhaba bulutta çalıştırırken hello aşağıdaki kullanın [değişken] ve [RoleInstanceValue] öğeleri:

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

## <a name="next-steps"></a>Sonraki adımlar
Bilgi nasıl tooperform bazı [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md) bulut hizmetiniz ile.

[Paket](cloud-services-model-and-package.md) bulut hizmetiniz.  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[görev]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[başlangıç]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[çalışma zamanı]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[ortam]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[değişken]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
