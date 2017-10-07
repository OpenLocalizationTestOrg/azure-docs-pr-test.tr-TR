---
title: "Varolan bir yürütülebilir tooAzure Service Fabric aaaDeploy | Microsoft Docs"
description: "Var olan bir uygulamayı, böylece bir konuk yürütülebilir olarak toopackage tooa Service Fabric kümesi nasıl dağıtılacağını üzerinde gözden geçirme"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Bir konuk yürütülebilir tooService doku dağıtma
Azure Service Fabric kod, Node.js, Java ya da C++ gibi herhangi bir türde bir hizmet olarak çalıştırabilirsiniz. Service Fabric toothese türlerdeki Hizmetleri Konuk yürütülebilir dosyalar ifade eder.

Konuk yürütülebilir dosyalar gibi durum bilgisi olmayan hizmetler Service Fabric tarafından kabul edilir. Sonuç olarak, bunlar kullanılabilirlik ve diğer ölçümleri temelinde, bir kümedeki düğümlere yerleştirilir. Bu makalede nasıl toopackage ve Visual Studio veya komut satırı yardımcı programını kullanarak bir konuk yürütülebilir tooa Service Fabric kümesi dağıtabilirsiniz.

Bu makalede, hello adımları toopackage yürütülebilir Konuk kapsar ve tooService doku dağıtın.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Service Fabric yürütülebilir Konuk çalıştıran avantajları
Bir Service Fabric kümesi yürütülebilir Konuk birkaç avantaj toorunning vardır:

* Yüksek kullanılabilirlik. Service Fabric çalışan uygulamaları yüksek oranda kullanılabilir hale getirilir. Service Fabric uygulaması örneğini çalıştırmasını sağlar.
* Sistem durumu izleme. Service Fabric sistem durumu izleme uygulama çalışıp çalışmadığını ve bir hata olduğunda tanılama bilgileri sağlayan olmadığını algılar.   
* Uygulama yaşam döngüsü yönetimi. Yükseltme sırasında bildirilen hatalı sistem durumu olayı ise yükseltmeler kapalı kalma süresi ile sağlamanın yanı sıra, Service Fabric otomatik geri alma toohello önceki sürümünü sağlar.    
* Yoğunluğu. Her uygulama toorun kendi donanımda hello ihtiyacını ortadan kaldıran bir kümede birden çok uygulama çalıştırabilirsiniz.
* Bulunabilirliği: REST kullanarak hello kümedeki diğer hizmetler hello Service Fabric adlandırma hizmeti toofind çağırabilirsiniz. 

## <a name="samples"></a>Örnekler
* [Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Uygulama ve hizmet bildirim dosyaları'na genel bakış
Bir konuk yürütülebilir dağıtma bir parçası olarak yararlı toounderstand hello Service Fabric paketleme ve dağıtım modeli açıklandığı gibi olmasından [uygulama modeli](service-fabric-application-model.md). Hello Service Fabric paketleme model üzerinde iki XML dosyasını kullanır: uygulama ve hizmet bildirimlerini hello. Merhaba şema tanımı hello ApplicationManifest.xml ve ServiceManifest.xml dosyaları yüklü olduğunda ile Merhaba Service Fabric SDK içine *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Uygulama bildirimini** hello uygulama bildirimidir kullanılan toodescribe Merhaba uygulaması. Onu oluşturan hello Hizmetleri ve örnek hello sayısı gibi nasıl bir veya daha fazla hizmet dağıtılmalıdır kullanılan toodefine olan diğer parametreleri listeler.

  Service Fabric bir uygulama dağıtımı ve yükseltmesi birimidir. Bir uygulama olası hataları ve olası düzeyine yönetildiği tek bir birim olarak yükseltilebilir. Service Fabric garanti hello yükseltme işlemi şunlardan biri olduğundan başarılı ya da hello yükseltme başarısız olursa Merhaba uygulaması bilinmeyen veya kararsız bir durumda bırakmaz.
* **Hizmet bildirimi** hello hizmet bildirimi hello hizmet bileşenlerinin açıklar. Merhaba adı ve hizmet türü gibi veri ve kod ve yapılandırma içerir. Merhaba hizmet bildirimi de olabilecek bazı ek parametreleri içeren tooconfigure hello hizmet dağıtıldıktan sonra kullanılacak.

## <a name="application-package-file-structure"></a>Uygulama paketi dosya yapısı
bir uygulama tooService doku toodeploy Merhaba uygulaması tanımlanmış dizin yapısına uygun olmalıdır. Merhaba, bu yapıyı örneği verilmiştir.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Merhaba ApplicationPackageRoot Merhaba uygulaması tanımlayan hello ApplicationManifest.xml dosyası içerir. Merhaba uygulamasına dahil edilen her hizmet için bir alt tüm hello hizmeti gerektiren yapıları hello kullanılan toocontain ' dir. Bu alt dizinlere hello ServiceManifest.xml ve genellikle aşağıdaki hello şunlardır:

* *Kod*. Bu dizin hello servis kodunu içerir.
* *Config*. Bu dizin, hello hizmeti çalışma zamanı tooretrieve belirli yapılandırma ayarları erişebilmesini Settings.xml dosya (ve gerekirse diğer dosyaları) içerir.
* *Veri*. Merhaba hizmeti gereken bir ek dizin toostore ek yerel veri budur. Veri kullanılan toostore yalnızca geçici veri olması gerekir. Merhaba hizmetinin (örneğin, yük devretme sırasında) yeniden konumlandırılmasını toobe gerekirse Service Fabric değil kopyalama veya çoğaltılacak değişiklikleri toohello veri dizini yok.

> [!NOTE]
> Toocreate hello yok `config` ve `data` ihtiyaç duymuyorsanız dizinleri.
>
>

## <a name="package-an-existing-executable"></a>Paketin var olan bir yürütülebilir dosya
Bir konuk yürütülebilir paketleme, Visual Studio Proje şablonu ya da toouse seçebilirsiniz veya çok[hello uygulama paketini el ile oluşturmak](#manually). Visual Studio kullanarak, uygulama paketinin yapısı hello ve bildirim dosyası hello yeni proje şablonu tarafından sizin için oluşturulur.

> [!TIP]
> Merhaba en kolay yolu toopackage bir hizmete yürütülebilir bir mevcut Windows olduğu toouse Visual Studio ve Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Visual Studio toopackage kullanın ve var olan bir yürütülebilir dosya dağıtma
Visual Studio Service Fabric Konuk yürütülebilir tooa Service Fabric küme dağıtma hizmet şablonu toohelp sağlar.

1. Seçin **dosya** > **yeni proje**ve bir Service Fabric uygulaması oluşturun.
2. Seçin **Konuk yürütülebilir** hello hizmet şablonu olarak.
3. Tıklatın **Gözat** tooselect hello klasörüyle çalıştırılabilir ve hello rest hello parametreleri toocreate hello hizmetinin doldurun.
   * *Kod paketi davranış*. Set toocopy hello yürütülebilir değişmezse faydalı olan, klasör toohello Visual Studio projesi, tüm başlangıç içeriğini olabilir. Hello yürütülebilir toochange beklediğiniz ve dinamik olarak hello özelliği toopick yeni yapılar yedeklemek istiyorsanız, bunun yerine toolink toohello klasör seçebilirsiniz. Visual Studio'da hello uygulama projesi oluştururken, bağlantılı klasörleri kullanabilirsiniz. Bu toohello kaynak konumdan yürütülebilir kaynak hedefine, tooupdate hello Konuk için olası kolaylaştırarak hello projede bağlar. Bu güncelleştirmeler derlemede hello uygulama paketinin parçası haline gelir.
   * *Program* toostart hello hizmet çalıştırılmalıdır hello yürütülebilir dosya belirtir.
   * *Bağımsız değişkenler* toohello yürütülebilir iletilmesi gereken hello bağımsız değişkenlerini belirtir. Bağımsız değişkenlerle parametrelerin listesi olabilir.
   * *WorkingFolder* başlatılan toobe geçiyor hello işlem hello çalışma dizini belirtir. Üç değerleri belirtebilirsiniz:
     * `CodeBase`Bu hello çalışma dizini toobe hello uygulama paketinde toohello kod dizini ayarlanmış olduğuna belirtir (`Code` dosya yapısı önceki hello gösterilen dizin).
     * `CodePackage`Bu hello çalışma dizini toobe ayarlamak toohello kök hello uygulama paketinin olduğuna belirtir (`GuestService1Pkg` dosya yapısı önceki hello gösterilen).
     * `Work`Merhaba dosyaları iş adlı bir alt dizinde yerleştirileceğini belirler.
4. Hizmetinize bir ad verin ve **Tamam**’a tıklayın.
5. Hizmet iletişimi için bir uç nokta gerekiyorsa, artık hello protokolü, bağlantı noktası ve türü toohello ServiceManifest.xml dosya ekleyebilirsiniz. Örneğin: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Şimdi, hello paketini kullanmak ve eylem hello çözümü Visual Studio'da hata ayıklama yerel kümenizdeki karşı yayımlayın. Hazır olduğunuzda, yayımlama hello uygulama tooa uzaktan küme veya hello çözüm toosource denetiminde denetleyin.
7. Bu makale toosee toohello sonuna nasıl Git tooview Service Fabric Explorer'da çalıştıran Konuk yürütülebilir hizmetinizi.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Yoeman toopackage kullanın ve var olan bir yürütülebilir dosya Linux'ta dağıtma

oluşturma ve dağıtma Linux'ta yürütülebilir Konuk hello yordamı olduğu hello csharp veya java uygulamasını dağıtma aynı.

1. Bir terminal penceresinde `yo azuresfguest` yazın.
2. Uygulamanızı adlandırın.
3. Hizmet adı ve hello yürütülebilir dosya yolu ve hello parametreleri ile çağrılmalıdır gibi hello ayrıntıları sağlayın.

Yeoman hello uygun uygulama ile bir uygulama paketi oluşturur ve bildirim dosyası ile birlikte yüklemek ve komut dosyaları kaldırmak.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>El ile paketini ve varolan yürütülebilir bir dağıtma
bir konuk yürütülebilir dosyayı el ile paketleme hello işlemi aşağıdaki genel adımları hello üzerinde dayanır:

1. Merhaba paket dizin yapısını oluşturun.
2. Merhaba uygulamanın kod ve yapılandırma dosyalarını ekleyin.
3. Merhaba hizmet bildirim dosyasını düzenleyin.
4. Merhaba uygulama bildirim dosyasının düzenleyin.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Merhaba paket dizin yapısını oluşturun
Merhaba dizin yapısını oluşturarak bölümünde, önceki hello açıklandığı gibi başlatabilirsiniz "Uygulama paketi dosya yapısı."

### <a name="add-hello-applications-code-and-configuration-files"></a>Merhaba uygulamanın kod ve yapılandırma dosyaları Ekle
Merhaba dizin yapısını oluşturduktan sonra hello kod ve yapılandırma dizinleri altında hello uygulamanın kod ve yapılandırma dosyaları ekleyebilirsiniz. Ek dizinler veya hello kod veya yapılandırma dizinleri alt dizinler de oluşturabilirsiniz.

Service Fabric mu bir `xcopy` hello içeriğiyle nedenle iki üst dizini, kod ve ayarları oluşturma dışında hiçbir önceden tanımlanmış yapısı toouse hello uygulama kök dizini. (Dilerseniz farklı adlar seçim yapabilirsiniz. Daha fazla ayrıntı hello sonraki bölümünde bulunur.)

> [!NOTE]
> Tüm hello dosyaları ve uygulama gereksinimlerini hello bağımlılıkları eklediğinizden emin olun. Service Fabric hello uygulamanın Hizmetleri dağıtılan giderek toobe nerede hello kümede hello tüm düğümlerde hello uygulama paketi içeriği kopyalar. Merhaba paket Merhaba uygulaması toorun ihtiyaç duyduğu tüm hello kodu içermelidir. Merhaba bağımlılıkları zaten kurulu olduğunu varsayın değil.
>
>

### <a name="edit-hello-service-manifest-file"></a>Merhaba hizmet bildirim dosyasını düzenleyin
Hello sonraki adıma tooedit hello hizmet bildirim dosyası tooinclude hello bilgi aşağıdaki gibidir:

* Merhaba hizmet türünün Hello adı. Bu, Service Fabric tooidentify bir hizmeti kullanan bir kimliğidir.
* Merhaba komutu toouse toolaunch hello uygulaması (ExeHost).
* Toobe gereken komut dosyaları tooset hello uygulamasının (SetupEntrypoint) çalıştırın.

Merhaba örneği aşağıdadır bir `ServiceManifest.xml` dosyası:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Aşağıdaki bölümlerde hello hello farklı kısımlarını tooupdate gerektiğini hello dosya gidin.

#### <a name="update-servicetypes"></a>Güncelleştirme ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* İstediğiniz herhangi bir ad seçin `ServiceTypeName`. Merhaba değeri hello kullanılan `ApplicationManifest.xml` dosya tooidentify hello hizmeti.
* Belirtin `UseImplicitHost="true"`. Bu öznitelik Service Fabric söyler hello hizmeti kendi başına bir uygulama üzerinde temel, gerekli tüm Service Fabric toolaunch toodo olduğundan bir işlem olarak ve durumunu izleyin.

#### <a name="update-codepackage"></a>CodePackage güncelleştir
Merhaba CodePackage öğesi hello hizmetin kod hello konumu (ve sürüm) belirtir.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Merhaba `Name` öğesidir hello directory hello uygulama hello hizmetin kodu içeren bir paket içinde kullanılan toospecify hello adı. `CodePackage`Ayrıca hello sahip `version` özniteliği. Bu kullanılan toospecify hello hello kod sürümü olabilir ve aynı zamanda potansiyel olabilir Service Fabric hello uygulama yaşam döngüsü yönetimi altyapısını kullanarak tooupgrade hello hizmetin kod kullanılır.

#### <a name="optional-update-setupentrypoint"></a>İsteğe bağlı: Güncelleştirme SetupEntrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
Merhaba SetupEntryPoint öğesi kullanılan toospecify hello hizmetin kod başlatılmadan önce yürütülüp herhangi çalıştırılabilir veya toplu iş dosyasıdır. Başlatma gerekli ise dahil toobe gerek kalmayacak şekilde isteğe bağlı bir adım var. Merhaba hizmeti her başlatıldığında hello SetupEntryPoint yürütülür.

Olmadığından tek SetupEntryPoint Kurulum betikleri hello uygulamanın kurulum birden çok komut dosyası gerektiriyorsa tek toplu iş dosyasında gruplandırılmış toobe gerekir. Merhaba SetupEntryPoint tüm dosya türlerinin yürütebilirsiniz: yürütülebilir dosyaları, toplu iş dosyaları ve PowerShell cmdlet'leri. Daha fazla ayrıntı için bkz: [yapılandırma SetupEntryPoint](service-fabric-application-runas-security.md).

Örnek önceki hello hello SetupEntryPoint adlı bir toplu iş dosyasını çalıştırır `LaunchConfig.cmd` diğer bir deyişle bulunan hello `scripts` alt hello kod dizini (Merhaba WorkingFolder öğesi tooCodeBase ayarlanmış olduğu varsayılarak).

#### <a name="update-entrypoint"></a>EntryPoint güncelleştir
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Merhaba `EntryPoint` hello hizmet bildirim dosyasında öğedir kullanılan toospecify nasıl toolaunch hello hizmet. Merhaba `ExeHost` öğesi belirttiğinden hello yürütülebilir (ve bağımsız değişkenler) olması gereken toolaunch hello hizmeti kullanılır.

* `Program`Merhaba hello hizmet başlaması gereken hello yürütülebilir dosyanın adını belirtir.
* `Arguments`toohello yürütülebilir iletilmesi gereken hello bağımsız değişkenlerini belirtir. Bağımsız değişkenlerle parametrelerin listesi olabilir.
* `WorkingFolder`başlatılan toobe geçiyor hello işlem Hello çalışma dizini belirtir. Üç değerleri belirtebilirsiniz:
  * `CodeBase`Bu hello çalışma dizini toobe hello uygulama paketinde toohello kod dizini ayarlanmış olduğuna belirtir (`Code` dosya yapısı önceki hello dizin).
  * `CodePackage`Bu hello çalışma dizini toobe ayarlamak toohello kök hello uygulama paketinin olduğuna belirtir (`GuestService1Pkg` dosya yapısı önceki hello içinde).
    * `Work`Merhaba dosyaları iş adlı bir alt dizinde yerleştirileceğini belirler.

Merhaba WorkingFolder yararlı tooset hello doğru çalışma dizini, böylelikle göreli yollar ya da hello uygulama veya başlatma komut dosyaları tarafından kullanılabilir.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Uç noktaları güncelleştirin ve iletişim için adlandırma hizmetine kaydetme
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
Örnek önceki hello hello `Endpoint` öğesi Merhaba uygulaması üzerinde dinleme hello uç noktalarını belirtir. Bu örnekte, hello Node.js uygulaması HTTP 3000 bağlantı noktasında dinler.

Ayrıca diğer hizmetler hello uç noktası adresi toothis hizmeti bulabilir şekilde Bu uç nokta toohello Naming Service Service Fabric toopublish sorabilirsiniz. Bu, Konuk yürütülebilir hizmetleri arasında toobe mümkün toocommunicate sağlar.
Merhaba yayımlanan uç noktası adresi hello biçimidir `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme`ve `PathSuffix` isteğe bağlı öznitelikleri. `IPAddressOrFQDN`IP adresi veya tam etki alanı adı bu yürütülebilir dosya üzerine yerleştirilen hello düğümünün hello ve sizin için hesaplanır ' dir.

Merhaba aşağıdaki örnekte, bir kez hello hizmet dağıtılır, Service Fabric Explorer'da benzer bir uç nokta çok gördüğünüz`http://10.1.4.92:3000/myapp/` hello hizmet örneği için yayımlanan. Veya yerel makine varsa gördüğünüz `http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Bu adresleri ile kullanabileceğiniz [ters proxy](service-fabric-reverseproxy.md) toocommunicate hizmetleri arasında.

### <a name="edit-hello-application-manifest-file"></a>Merhaba uygulama bildirim dosyasının Düzenle
Merhaba yapılandırdıktan sonra `Servicemanifest.xml` dosya, bazı değişiklikler toohello toomake gerek `ApplicationManifest.xml` hello tooensure doğru hizmet türü ve adı kullanılan dosya.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
Merhaba, `ServiceManifestImport` öğesi hello uygulamasında tooinclude istediğiniz bir veya daha fazla hizmet belirtebilirsiniz. Hizmetleri ile başvurulan `ServiceManifestName`, hello burada hello hello dizinin adını belirtir `ServiceManifest.xml` dosyasının bulunduğu.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Günlük ayarlama
Hello uygulama ve yapılandırma betikleri hataları göster Konuk yürütülebilir dosyaları için bu yararlı toobe mümkün toosee konsol günlükleri toofind çıkışı olur.
Konsol yeniden yönlendirmesi hello yapılandırılabilir `ServiceManifest.xml` hello kullanarak dosyayı `ConsoleRedirection` öğesi.

> [!WARNING]
> Hiçbir zaman bu hello uygulama yük devretme etkileyebileceğinden üretimde dağıtılan bir uygulamada hello konsol yeniden yönlendirme ilkesi kullanın. *Yalnızca* bunu yerel geliştirme ve hata ayıklama amacıyla kullanın.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`kullanılan tooredirect konsol çıkış (stdout ve stderr) tooa çalışma dizini olabilir. Bu hatalar hiçbir hello Kurulum veya hello Service Fabric kümesi hello uygulamada yürütülmesi sırasında hello özelliği tooverify sağlar.

`FileRetentionCount`kaç tane dosyaları hello çalışma dizinindeki kaydedilir belirler. Örneğin, 5, değeri hello önceki beş yürütmeleri için hello günlük dosyalarını hello çalışma dizininde depolanır anlamına gelir.

`FileMaxSizeInKb`Merhaba hello günlük dosyalarının en büyük boyutunu belirtir.

Günlük dosyaları hello hizmetin çalışma dizinleri birinde kaydedilir. Merhaba dosyalarının bulunduğu toodetermine hangi düğümün hello hizmetinin çalıştığını ve hangi çalışma dizini kullanılan Service Fabric Explorer toodetermine kullanın. Bu işlem, bu makalenin sonraki bölümlerinde ele alınmaktadır.

## <a name="deployment"></a>Dağıtım
Merhaba son adımdır çok[uygulamanızı dağıtmak](service-fabric-deploy-remove-applications.md). PowerShell komut dosyası gösterilmektedir nasıl aşağıdaki hello toodeploy uygulama toohello yerel geliştirme küme ve yeni bir Service Fabric hizmetini başlatın.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Merhaba paket Sıkıştır](service-fabric-package-apps.md#compress-a-package) hello paketi büyük veya çok sayıda dosya varsa toohello Image store kopyalamadan önce. Daha fazla bilgi [burada](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Service Fabric hizmeti çeşitli "yapılandırmalarında." dağıtılabilir Örneğin, tek veya birden çok örneği dağıtılabilir veya hello Service Fabric kümesinin her bir düğümde hello Hizmeti'nin bir örneğini olduğunu şekilde dağıtılabilir.

Merhaba `InstanceCount` hello parametresinin `New-ServiceFabricService` cmdlet'tir kullanılan toospecify kaç tane hello hizmet örneğinin hello Service Fabric kümesi içinde başlatılan. Merhaba ayarlayabilirsiniz `InstanceCount` hello dağıtmakta olduğunuz uygulama türüne bağlı olarak değeri. Merhaba iki en yaygın senaryolar şunlardır:

* `InstanceCount = "1"`. Bu durumda, hello hizmetinin yalnızca bir örneğini hello kümede dağıtılır. Service Fabric'ın Zamanlayıcı hangi düğüm hello hizmeti dağıtılan toobe geçiyor belirler.
* `InstanceCount ="-1"`. Bu durumda, hello Hizmeti'nin bir örneğini hello Service Fabric kümedeki her düğümde dağıtılır. Merhaba sonuç hello hizmetinin her düğüm için bir (ve yalnızca bir) örneğini hello kümede yaşıyor.

İstemci uygulamaları çok "Merhaba küme toouse hello uç noktası hello düğümler tooany bağlanmak" ön uç uygulamalar (örneğin, bir REST uç noktası), için kullanışlı bir yapılandırma olmasıdır. Merhaba Service Fabric kümesinin tüm düğümlerine bağlı tooa yük dengeleyici olduğunda, örneğin, bu yapılandırma de kullanılabilir. İstemci trafiğini sonra hello kümedeki tüm düğümler üzerinde çalışan hello hizmeti üzerinden dağıtılabilir.

## <a name="check-your-running-application"></a>Çalışan uygulamanızı denetleyin
Service Fabric Explorer'da hello hizmetinin çalıştığı hello düğümü tanımlayın. Bu örnekte, Düğüm1 üzerinde çalışır:

![Hizmetinin çalıştığı düğüm](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Toohello düğümüne gidin ve toohello uygulama göz atın, diskteki konumuna dahil olmak üzere hello temel düğüm bilgileri görebilirsiniz.

![Disk konumu](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Sunucu Gezgini kullanarak toohello dizin göz atarsanız, hello ekran aşağıdaki gösterildiği gibi hello çalışma dizinini ve hello hizmetin Günlük klasörü bulabilirsiniz: 

![Günlük konumu](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrendiğiniz nasıl toopackage Konuk çalıştırılabilir ve tooService doku dağıtın. Merhaba makaleler ilgili bilgi ve görevler için bkz.

* [Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), bağlantı toohello yayın öncesi hello paketleme Aracı'nın dahil
* [İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Konuk tarafından yürütülebilir birden çok uygulama dağıtma](service-fabric-deploy-multiple-apps.md)
* [Visual Studio kullanarak ilk Service Fabric uygulamanızı oluşturma](service-fabric-create-your-first-application-in-visual-studio.md)
