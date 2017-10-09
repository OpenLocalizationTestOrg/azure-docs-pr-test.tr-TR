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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Önceki Java Service Fabric uygulaması toofetch Java kitaplıklarından Maven güncelleştir
Biz yakın zamanda Service Fabric Java ikili dosyaları hello Service Fabric Java SDK tooMaven barındırmasını taşınmış. Kullanabileceğiniz artık **mavencentral** toofetch hello en son hizmet doku Java bağımlılıkları. Service Fabric Java ya da Yeoman kullanarak SDK ile kullanılan şablon veya Eclipse, toobe dayalı Maven derleme hello ile uyumlu toobe daha önce oluşturduğunuz, varolan Java uygulamaları güncelleştirme bu hızlı başlangıç yardımcı olur.

## <a name="prerequisites"></a>Ön koşullar
1. İlk toouninstall ihtiyacınız var olan Java SDK'sı hello.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Yükleme hello en son hizmet doku CLI aşağıda belirtilen adımları hello [burada](service-fabric-cli.md).

3. toobuild ve iş hello Service Fabric Java uygulamaları, JDK 1.8 varsa ve Gradle yüklü tooensure gerekir. Henüz yüklü değilse, çalıştırabilirsiniz JDK 1.8 (openjdk-8-jdk) ve Gradle - tooinstall hello

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Güncelleştirme hello yükleme/kaldırma kodlarının uygulama toouse hello bahsedilen hello adımları izleyerek yeni hizmet doku CLI [burada](service-fabric-application-lifecycle-sfctl.md). Tooour başlama başvurabilir [örnekler](https://github.com/Azure-Samples/service-fabric-java-getting-started) başvuru.

>[!TIP]
> Merhaba Service Fabric Java SDK'ı kaldırdıktan sonra Yeoman çalışmaz. Belirtilen hello önkoşulları uyguladıktan [burada](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java şablonu oluşturucuyu oluşturan ve çalışma.

## <a name="service-fabric-java-libraries-on-maven"></a>Maven'da Service Fabric Java kitaplıkları
Maven’da barındırılan Service Fabric Java kitaplıkları. Hello hello bağımlılıklar ekleyebilirsiniz ``pom.xml`` veya ``build.gradle`` projeleri toouse Service Fabric Java kitaplıklarından birini **mavenCentral**.

### <a name="actors"></a>Aktörler

Uygulamanız için Service Fabric Güvenilir Aktör desteği.

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

### <a name="services"></a>Hizmetler

Uygulamanız için Service Fabric Durum Bilgisi Olmayan Hizmet desteği.

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

### <a name="others"></a>Diğer
#### <a name="transport"></a>Aktarım

Service Fabric Java uygulaması için Aktarım katmanı desteği. İhtiyacınız olmayan tooexplicitly, bu bağımlılık tooyour güvenilir aktör ya da hizmet uygulamaları hello aktarım katmanında program sürece ekleyin.

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

#### <a name="fabric-support"></a>Fabric desteği

Sistem düzeyinde toonative Service Fabric çalışma zamanı ettiği Service Fabric desteği. İhtiyacınız olmayan tooexplicitly eklemek bu bağımlılık tooyour güvenilir aktör veya hizmet uygulamaları. Bu otomatik olarak Maven alınan, eklediğiniz zaman yukarıdaki başka bir bağımlılık hello.

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


## <a name="migrating-service-fabric-stateless-service"></a>Microsoft Azure Service Fabric Durum Bilgisi Olmayan Hizmeti Geçirme

Service Fabric bağımlılıkları Maven alınan kullanarak var olan Service Fabric durum bilgisiz Java hizmetinizin tooupdate hello ihtiyacınız toobe mümkün toobuild ``build.gradle`` hello Service içindeki dosya. Daha önce toobe gibi aşağıdaki gibi kullanılacağını-
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
Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir
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
Genel olarak, tooget nasıl hello yapı komut dosyası hakkında genel bir fikir için Service Fabric durum bilgisiz Java hizmet gibidir, başlama örneklerimizde tooany örnek başvurabilir. Merhaba işte [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) hello EchoServer örnek.

## <a name="migrating-service-fabric-actor-service"></a>Service Fabric Aktör Hizmetini Geçirme

Service Fabric bağımlılıkları Maven alınan kullanarak, varolan Service Fabric aktör Java uygulaması tooupdate hello ihtiyacınız toobe mümkün toobuild ``build.gradle`` hello arabirimi paketin içindeki ve hello hizmet paketi dosyasının. TestClient paketiniz varsa, bu da tooupdate gerekir. Bunu, aktör için ``Myactor``, hello aşağıdaki ihtiyaç duyacağınız tooupdate - hello yerler olacaktır
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Derleme betiğinin hello arabirimi projesi için güncelleştirme

Daha önce toobe gibi aşağıdaki gibi kullanılacağını-
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir
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

#### <a name="updating-build-script-for-hello-actor-project"></a>Derleme betiğinin hello aktör projesi için güncelleştirme

Daha önce toobe gibi aşağıdaki gibi kullanılacağını-
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
Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir
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

#### <a name="updating-build-script-for-hello-test-client-project"></a>Derleme betiğinin hello test istemci projesi için güncelleştirme

Burada değişiklik önceki bölümde, diğer bir deyişle, hello aktör proje açıklanan benzer toohello değişir. Daha önce kullanılan komut dosyası toobe gibi aşağıdaki gibi Gradle hello-
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
Şimdi, Maven toofetch hello bağımlılıklardan hello **güncelleştirilmiş** ``build.gradle`` hello ilgili bölümleri gibi - gerekir
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

## <a name="next-steps"></a>Sonraki adımlar

* [Linux üzerinde Yeoman kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-create-your-first-linux-application-with-java.md)
* [Linux üzerinde Eclipse için Service Fabric Eklentisi kullanarak ilk Service Fabric Java uygulamanızı oluşturma ve dağıtma](service-fabric-get-started-eclipse.md)
* [Merhaba Service Fabric CLI kullanarak Service Fabric kümeleri ile etkileşim](service-fabric-cli.md)
