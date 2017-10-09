---
title: "Java SDK'sı tooMaven - gelen aaaMigrate güncelleştirme eski Azure Service Fabric Java uygulamaları toouse Maven | Microsoft Docs"
description: "Toouse hello Service Fabric Java SDK, kullanılan hello eski Java uygulamalarını toofetch Service Fabric Java Maven bağımlılıklardan güncelleştirin. Bu kurulum tamamlandıktan sonra eski Java uygulamalarınızı mümkün toobuild olacaktır."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="f07d1-104">Önceki Java Service Fabric uygulaması toofetch Java kitaplıklarından Maven güncelleştir</span><span class="sxs-lookup"><span data-stu-id="f07d1-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="f07d1-105">Biz yakın zamanda Service Fabric Java ikili dosyaları hello Service Fabric Java SDK tooMaven barındırmasını taşınmış.</span><span class="sxs-lookup"><span data-stu-id="f07d1-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="f07d1-106">Kullanabileceğiniz artık **mavencentral** toofetch hello en son hizmet doku Java bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="f07d1-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="f07d1-107">Service Fabric Java ya da Yeoman kullanarak SDK ile kullanılan şablon veya Eclipse, toobe dayalı Maven derleme hello ile uyumlu toobe daha önce oluşturduğunuz, varolan Java uygulamaları güncelleştirme bu hızlı başlangıç yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f07d1-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f07d1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f07d1-108">Prerequisites</span></span>
1. <span data-ttu-id="f07d1-109">İlk toouninstall ihtiyacınız var olan Java SDK'sı hello.</span><span class="sxs-lookup"><span data-stu-id="f07d1-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="f07d1-110">Yükleme hello en son hizmet doku CLI aşağıda belirtilen adımları hello [burada](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f07d1-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="f07d1-111">toobuild ve iş hello Service Fabric Java uygulamaları, JDK 1.8 varsa ve Gradle yüklü tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="f07d1-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="f07d1-112">Henüz yüklü değilse, çalıştırabilirsiniz JDK 1.8 (openjdk-8-jdk) ve Gradle - tooinstall hello</span><span class="sxs-lookup"><span data-stu-id="f07d1-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="f07d1-113">Güncelleştirme hello yükleme/kaldırma kodlarının uygulama toouse hello bahsedilen hello adımları izleyerek yeni hizmet doku CLI [burada](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="f07d1-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="f07d1-114">Tooour başlama başvurabilir [örnekler](https://github.com/Azure-Samples/service-fabric-java-getting-started) başvuru.</span><span class="sxs-lookup"><span data-stu-id="f07d1-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="f07d1-115">Merhaba Service Fabric Java SDK'ı kaldırdıktan sonra Yeoman çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f07d1-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="f07d1-116">Belirtilen hello önkoşulları uyguladıktan [burada](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java şablonu oluşturucuyu oluşturan ve çalışma.</span><span class="sxs-lookup"><span data-stu-id="f07d1-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="f07d1-117">Maven'da Service Fabric Java kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="f07d1-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="f07d1-118">Maven’da barındırılan Service Fabric Java kitaplıkları.</span><span class="sxs-lookup"><span data-stu-id="f07d1-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="f07d1-119">Hello hello bağımlılıklar ekleyebilirsiniz ``pom.xml`` veya ``build.gradle`` projeleri toouse Service Fabric Java kitaplıklarından birini **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="f07d1-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="f07d1-120">Aktörler</span><span class="sxs-lookup"><span data-stu-id="f07d1-120">Actors</span></span>

<span data-ttu-id="f07d1-121">Uygulamanız için Service Fabric Güvenilir Aktör desteği.</span><span class="sxs-lookup"><span data-stu-id="f07d1-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="f07d1-122">Hizmetler</span><span class="sxs-lookup"><span data-stu-id="f07d1-122">Services</span></span>

<span data-ttu-id="f07d1-123">Uygulamanız için Service Fabric Durum Bilgisi Olmayan Hizmet desteği.</span><span class="sxs-lookup"><span data-stu-id="f07d1-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="f07d1-124">Diğer</span><span class="sxs-lookup"><span data-stu-id="f07d1-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="f07d1-125">Aktarım</span><span class="sxs-lookup"><span data-stu-id="f07d1-125">Transport</span></span>

<span data-ttu-id="f07d1-126">Service Fabric Java uygulaması için Aktarım katmanı desteği.</span><span class="sxs-lookup"><span data-stu-id="f07d1-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="f07d1-127">İhtiyacınız olmayan tooexplicitly, bu bağımlılık tooyour güvenilir aktör ya da hizmet uygulamaları hello aktarım katmanında program sürece ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f07d1-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="f07d1-128">Fabric desteği</span><span class="sxs-lookup"><span data-stu-id="f07d1-128">Fabric support</span></span>

<span data-ttu-id="f07d1-129">Sistem düzeyinde toonative Service Fabric çalışma zamanı ettiği Service Fabric desteği.</span><span class="sxs-lookup"><span data-stu-id="f07d1-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="f07d1-130">İhtiyacınız olmayan tooexplicitly eklemek bu bağımlılık tooyour güvenilir aktör veya hizmet uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="f07d1-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="f07d1-131">Bu otomatik olarak Maven alınan, eklediğiniz zaman yukarıdaki başka bir bağımlılık hello.</span><span class="sxs-lookup"><span data-stu-id="f07d1-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="f07d1-132">Microsoft Azure Service Fabric Durum Bilgisi Olmayan Hizmeti Geçirme</span><span class="sxs-lookup"><span data-stu-id="f07d1-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="f07d1-133">Service Fabric bağımlılıkları Maven alınan kullanarak var olan Service Fabric durum bilgisiz Java hizmetinizin tooupdate hello ihtiyacınız toobe mümkün toobuild ``build.gradle`` hello Service içindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="f07d1-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="f07d1-134">Daha önce toobe gibi aşağıdaki gibi kullanılacağını-</span><span class="sxs-lookup"><span data-stu-id="f07d1-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="f07d1-135">Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir</span><span class="sxs-lookup"><span data-stu-id="f07d1-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="f07d1-136">Genel olarak, tooget nasıl hello yapı komut dosyası hakkında genel bir fikir için Service Fabric durum bilgisiz Java hizmet gibidir, başlama örneklerimizde tooany örnek başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="f07d1-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="f07d1-137">Merhaba işte [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) hello EchoServer örnek.</span><span class="sxs-lookup"><span data-stu-id="f07d1-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="f07d1-138">Service Fabric Aktör Hizmetini Geçirme</span><span class="sxs-lookup"><span data-stu-id="f07d1-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="f07d1-139">Service Fabric bağımlılıkları Maven alınan kullanarak, varolan Service Fabric aktör Java uygulaması tooupdate hello ihtiyacınız toobe mümkün toobuild ``build.gradle`` hello arabirimi paketin içindeki ve hello hizmet paketi dosyasının.</span><span class="sxs-lookup"><span data-stu-id="f07d1-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="f07d1-140">TestClient paketiniz varsa, bu da tooupdate gerekir.</span><span class="sxs-lookup"><span data-stu-id="f07d1-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="f07d1-141">Bunu, aktör için ``Myactor``, hello aşağıdaki ihtiyaç duyacağınız tooupdate - hello yerler olacaktır</span><span class="sxs-lookup"><span data-stu-id="f07d1-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="f07d1-142">Derleme betiğinin hello arabirimi projesi için güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f07d1-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="f07d1-143">Daha önce toobe gibi aşağıdaki gibi kullanılacağını-</span><span class="sxs-lookup"><span data-stu-id="f07d1-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="f07d1-144">Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir</span><span class="sxs-lookup"><span data-stu-id="f07d1-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="f07d1-145">Derleme betiğinin hello aktör projesi için güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f07d1-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="f07d1-146">Daha önce toobe gibi aşağıdaki gibi kullanılacağını-</span><span class="sxs-lookup"><span data-stu-id="f07d1-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="f07d1-147">Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir</span><span class="sxs-lookup"><span data-stu-id="f07d1-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="f07d1-148">Derleme betiğinin hello test istemci projesi için güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f07d1-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="f07d1-149">Burada değişiklik önceki bölümde, diğer bir deyişle, hello aktör proje açıklanan benzer toohello değişir.</span><span class="sxs-lookup"><span data-stu-id="f07d1-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="f07d1-150">Daha önce kullanılan komut dosyası toobe gibi aşağıdaki gibi Gradle hello-</span><span class="sxs-lookup"><span data-stu-id="f07d1-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="f07d1-151">Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir</span><span class="sxs-lookup"><span data-stu-id="f07d1-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="f07d1-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f07d1-152">Next steps</span></span>

* [<span data-ttu-id="f07d1-153">Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="f07d1-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="f07d1-154">Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="f07d1-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="f07d1-155">Merhaba Service Fabric CLI kullanarak Service Fabric kümeleri ile etkileşim</span><span class="sxs-lookup"><span data-stu-id="f07d1-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
