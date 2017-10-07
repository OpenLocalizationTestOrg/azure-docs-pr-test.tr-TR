---
title: "aaaApache örnek Java topolojisi - Azure Hdınsight Storm | Microsoft Docs"
description: "Bir örnek sözcük oluşturarak toocreate Apache Storm topolojilerini Java topolojisi nasıl saymak öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "Apache storm, apache storm örnek, storm java, storm topoloji örneği"
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="41a72-104">Apache Storm topolojisini Java oluşturma</span><span class="sxs-lookup"><span data-stu-id="41a72-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="41a72-105">Bilgi nasıl toocreate Apache Storm için Java tabanlı bir topolojiyi.</span><span class="sxs-lookup"><span data-stu-id="41a72-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="41a72-106">Word-count uygulama uygulayan bir Storm topolojisinin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41a72-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="41a72-107">Maven toobuild ve paket hello proje kullanın.</span><span class="sxs-lookup"><span data-stu-id="41a72-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="41a72-108">Daha sonra nasıl toodefine hello topolojisi kullanarak izin ver hello Flux framework öğrenin.</span><span class="sxs-lookup"><span data-stu-id="41a72-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="41a72-109">Merhaba Flux Storm 0.10.0 veya sonraki sürümlerinde çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="41a72-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="41a72-110">Storm 0.10.0 Hdınsight 3.3 ve 3.4 ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="41a72-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="41a72-111">Bu belgedeki Hello adımları tamamladıktan sonra hello topoloji tooApache Hdınsight üzerinde Storm dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41a72-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="41a72-112">Bu belgede oluşturulan hello Storm topolojisini örnekler tamamlanmış bir sürümünü şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="41a72-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41a72-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41a72-113">Prerequisites</span></span>

* [<span data-ttu-id="41a72-114">Java Geliştirme Seti (JDK) sürüm 7</span><span class="sxs-lookup"><span data-stu-id="41a72-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="41a72-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven Java projeleri için bir proje derleme sistemidir.</span><span class="sxs-lookup"><span data-stu-id="41a72-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="41a72-116">Bir metin düzenleyicisi veya IDE.</span><span class="sxs-lookup"><span data-stu-id="41a72-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="41a72-117">Ortam değişkenleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="41a72-117">Configure environment variables</span></span>

<span data-ttu-id="41a72-118">Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="41a72-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="41a72-119">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="41a72-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="41a72-120">**JAVA_HOME** -hello Java Çalışma zamanı ortamı (JRE) yüklü olduğu toohello dizin işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="41a72-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="41a72-121">Örneğin, bir UNIX veya Linux dağıtımlarında benzeri bir değer çok olması gereken`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="41a72-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="41a72-122">Windows'da onu benzeri bir değer çok gerekir`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="41a72-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="41a72-123">**YOL** -yolları aşağıdaki hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="41a72-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="41a72-124">**JAVA_HOME** (veya hello eşdeğer yolu)</span><span class="sxs-lookup"><span data-stu-id="41a72-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="41a72-125">**JAVA_HOME\bin** (veya hello eşdeğer yolu)</span><span class="sxs-lookup"><span data-stu-id="41a72-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="41a72-126">Maven'ın yüklendiği hello dizini</span><span class="sxs-lookup"><span data-stu-id="41a72-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="41a72-127">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="41a72-127">Create a Maven project</span></span>

<span data-ttu-id="41a72-128">Merhaba komut satırından kullanma hello aşağıdaki toocreate adlı bir Maven projesi komutu **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="41a72-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="41a72-129">PowerShell kullanıyorsanız, çevreleyen gerekir`-D` çift tırnak işareti parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="41a72-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="41a72-130">Bu komut adlı bir dizin oluşturur `WordCount` hello geçerli konumda içeren temel bir Maven projesi.</span><span class="sxs-lookup"><span data-stu-id="41a72-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="41a72-131">Merhaba `WordCount` dizini aşağıdaki öğelerindeki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="41a72-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="41a72-132">`pom.xml`: Merhaba Maven projesine ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="41a72-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="41a72-133">`src\main\java\com\microsoft\example`: Uygulama kodunuz içerir.</span><span class="sxs-lookup"><span data-stu-id="41a72-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="41a72-134">`src\test\java\com\microsoft\example`: Uygulamanız için testleri içerir.</span><span class="sxs-lookup"><span data-stu-id="41a72-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="41a72-135">Merhaba oluşturulan örnek kodu kaldırın</span><span class="sxs-lookup"><span data-stu-id="41a72-135">Remove hello generated example code</span></span>

<span data-ttu-id="41a72-136">Oluşturulan hello test ve hello uygulama dosyaları silin:</span><span class="sxs-lookup"><span data-stu-id="41a72-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="41a72-137">**src\test\java\com\microsoft\example\AppTest.Java**</span><span class="sxs-lookup"><span data-stu-id="41a72-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="41a72-138">**src\main\java\com\microsoft\example\App.Java**</span><span class="sxs-lookup"><span data-stu-id="41a72-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="41a72-139">Maven depoları ekleme</span><span class="sxs-lookup"><span data-stu-id="41a72-139">Add Maven repositories</span></span>

<span data-ttu-id="41a72-140">Hdınsight üzerinde hello Hortonworks veri Platformu (HDP) dayalı, bu yüzden hello Hortonworks depo toodownload bağımlılıkları Apache Storm projeleriniz için kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="41a72-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="41a72-141">Merhaba, __pom.xml__ dosya, XML hello sonra aşağıdaki hello eklemek `<url>http://maven.apache.org</url>` satır:</span><span class="sxs-lookup"><span data-stu-id="41a72-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="41a72-142">Özellikler ekleme</span><span class="sxs-lookup"><span data-stu-id="41a72-142">Add properties</span></span>

<span data-ttu-id="41a72-143">Maven özellikleri olarak adlandırılan toodefine proje düzeyi değerlere izin verir.</span><span class="sxs-lookup"><span data-stu-id="41a72-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="41a72-144">Merhaba, __pom.xml__, metin hello sonra aşağıdaki hello eklemek `</repositories>` satır:</span><span class="sxs-lookup"><span data-stu-id="41a72-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="41a72-145">Bu değer hello diğer bölümlerinde artık kullanabilirsiniz `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="41a72-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="41a72-146">Örneğin, Storm bileşenleri hello sürümü belirtirken kullanabileceğiniz `${storm.version}` sabit bir değer kodlama yerine.</span><span class="sxs-lookup"><span data-stu-id="41a72-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="41a72-147">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41a72-147">Add dependencies</span></span>

<span data-ttu-id="41a72-148">Storm bileşenleri için bağımlılık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41a72-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="41a72-149">Açık hello `pom.xml` dosya ve hello kodda aşağıdaki hello ekleyin `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="41a72-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="41a72-150">Bu bilgi toolook Maven derleme zamanında kullanan `storm-core` hello Maven deposundaki.</span><span class="sxs-lookup"><span data-stu-id="41a72-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="41a72-151">Yerel bilgisayarınızda hello deposundaki İlk bakar.</span><span class="sxs-lookup"><span data-stu-id="41a72-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="41a72-152">Merhaba dosyaları yoksa, Maven hello ortak Maven depodan indirir ve hello yerel depoda depolar.</span><span class="sxs-lookup"><span data-stu-id="41a72-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="41a72-153">Bildirim hello `<scope>provided</scope>` bu bölümdeki satır.</span><span class="sxs-lookup"><span data-stu-id="41a72-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="41a72-154">Bu ayar Maven tooexclude söyler **storm çekirdek** hello sistem tarafından sağlanan bulunduğundan, oluşturulan JAR dosyalarını.</span><span class="sxs-lookup"><span data-stu-id="41a72-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="41a72-155">Derleme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="41a72-155">Build configuration</span></span>

<span data-ttu-id="41a72-156">Maven eklentileri toocustomize hello derleme aşamaları hello projesinin izin verin.</span><span class="sxs-lookup"><span data-stu-id="41a72-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="41a72-157">Örneğin, nasıl hello Proje derlenir veya nasıl toopackage JAR dosyasını içine.</span><span class="sxs-lookup"><span data-stu-id="41a72-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="41a72-158">Açık hello `pom.xml` dosya ve doğrudan hello yukarıdaki kodu aşağıdaki hello ekleyin `</project>` satır.</span><span class="sxs-lookup"><span data-stu-id="41a72-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="41a72-159">Bu bölümde kullanılan tooadd eklentileri, kaynakları ve diğer yapı yapılandırma seçenekleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="41a72-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="41a72-160">Merhaba, tam başvuru için **pom.xml** dosya için bkz: [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="41a72-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="41a72-161">Eklentiler</span><span class="sxs-lookup"><span data-stu-id="41a72-161">Add plug-ins</span></span>

<span data-ttu-id="41a72-162">Java'da uygulanan Apache Storm topolojilerini için hello [Exec Maven eklentisi](http://www.mojohaus.org/exec-maven-plugin/) hello topolojisi geliştirme ortamınızı yerel olarak çalıştırma tooeasily izin verdiği için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="41a72-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="41a72-163">Toohello aşağıdaki hello eklemek `<plugins>` hello bölümünü `pom.xml` tooinclude hello Exec Maven eklenti dosyası:</span><span class="sxs-lookup"><span data-stu-id="41a72-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="41a72-164">Başka yararlı hello eklentidir [Apache Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/), hangi derleme seçenekleri kullanılan toochange değil.</span><span class="sxs-lookup"><span data-stu-id="41a72-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="41a72-165">Merhaba değişiklikleri hello kaynak ve hedef uygulamanız için Maven kullanımları Java sürümü hello.</span><span class="sxs-lookup"><span data-stu-id="41a72-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="41a72-166">Hdınsight için __3.4 veya önceki__hello kaynak ayarlamak ve Java Sürüm too__1.7__ hedef.</span><span class="sxs-lookup"><span data-stu-id="41a72-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="41a72-167">Hdınsight için __3.5__hello kaynak ayarlamak ve Java Sürüm too__1.8__ hedef.</span><span class="sxs-lookup"><span data-stu-id="41a72-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="41a72-168">Merhaba metinde aşağıdaki hello eklemek `<plugins>` hello bölümünü `pom.xml` tooinclude hello Apache Maven derleyici eklentisi dosya.</span><span class="sxs-lookup"><span data-stu-id="41a72-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="41a72-169">Merhaba hedef Hdınsight sürüm 3.5 olması için bu örnek 1.8, belirtir.</span><span class="sxs-lookup"><span data-stu-id="41a72-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="41a72-170">Kaynaklarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41a72-170">Configure resources</span></span>

<span data-ttu-id="41a72-171">Merhaba kaynakları bölümü hello topolojisinde bileşenleri tarafından gereken yapılandırma dosyaları gibi tooinclude kod olmayan kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="41a72-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="41a72-172">Bu örnekte, hello metinde aşağıdaki hello eklemek `<resources>` hello bölümünü ' pom.xml dosyasını.</span><span class="sxs-lookup"><span data-stu-id="41a72-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="41a72-173">Bu örnek hello kaynakları dizin hello hello proje kök dizininde ekler (`${basedir}`) kaynaklar içeriyor ve adlı hello dosya içeren bir konum olarak `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="41a72-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="41a72-174">Bu dosya kullanılan tooconfigure hello topolojisi tarafından hangi bilgilerin oturum açmış durumda.</span><span class="sxs-lookup"><span data-stu-id="41a72-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="41a72-175">Merhaba topolojisi oluştur</span><span class="sxs-lookup"><span data-stu-id="41a72-175">Create hello topology</span></span>

<span data-ttu-id="41a72-176">Java tabanlı Apache Storm topolojisini bağımlılık olarak yazmanız gerekir üç bileşeni (veya başvuru) oluşur.</span><span class="sxs-lookup"><span data-stu-id="41a72-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="41a72-177">**Spout'lar**: dış veri kaynakları ve veri akışları hello topoloji yayar okur.</span><span class="sxs-lookup"><span data-stu-id="41a72-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="41a72-178">**Cıvatalar**: spout'lar veya diğer Cıvatalar tarafından gösterilen akışları üzerinde işlemeyi gerçekleştirir ve bir veya daha fazla akışları yayar.</span><span class="sxs-lookup"><span data-stu-id="41a72-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="41a72-179">**Topoloji**: nasıl hello spout'lar ve Cıvatalar düzenlenir ve hello giriş noktası için hello topolojisi sunar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="41a72-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="41a72-180">Merhaba spout oluşturma</span><span class="sxs-lookup"><span data-stu-id="41a72-180">Create hello spout</span></span>

<span data-ttu-id="41a72-181">Dış veri kaynakları için tooreduce gereksinimler hello aşağıdaki spout yalnızca rastgele cümleleri yayar.</span><span class="sxs-lookup"><span data-stu-id="41a72-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="41a72-182">Merhaba ile sağlanan bir spout değiştirilmiş bir sürümünü olan [Storm Starter örnekleri](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="41a72-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="41a72-183">Bir dış veri kaynağından okur spout bir örnek için örnek hello birine bakın:</span><span class="sxs-lookup"><span data-stu-id="41a72-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="41a72-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): Twitter'dan okuyan bir örnek spout</span><span class="sxs-lookup"><span data-stu-id="41a72-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="41a72-185">[Storm Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): Kafka okur spout</span><span class="sxs-lookup"><span data-stu-id="41a72-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="41a72-186">Merhaba spout için adlı bir dosya oluşturun `RandomSentenceSpout.java` hello içinde `src\main\java\com\microsoft\example` hello içeriği Java kod aşağıdaki dizin ve kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="41a72-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="41a72-187">Bu topoloji yalnızca bir spout kullansa da, diğerlerinin hello topoloji farklı kaynaklardan veri akışı birkaç olabilir.</span><span class="sxs-lookup"><span data-stu-id="41a72-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="41a72-188">Merhaba Cıvatalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="41a72-188">Create hello bolts</span></span>

<span data-ttu-id="41a72-189">Cıvatalar hello veri işleme işleyin.</span><span class="sxs-lookup"><span data-stu-id="41a72-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="41a72-190">Bu topoloji iki Cıvatalar kullanır:</span><span class="sxs-lookup"><span data-stu-id="41a72-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="41a72-191">**SplitSentence**: böler tarafından gösterilen hello cümleleri **RandomSentenceSpout** ayrı sözcükleri içine.</span><span class="sxs-lookup"><span data-stu-id="41a72-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="41a72-192">**WordCount**: her sözcüğün oluştu kaç kez sayar.</span><span class="sxs-lookup"><span data-stu-id="41a72-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="41a72-193">Cıvatalar hiçbir şey, örneğin, hesaplama, sürdürme veya tooexternal bileşenleri Konuşmayı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41a72-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="41a72-194">İki yeni dosyalar oluşturma `SplitSentence.java` ve `WordCount.java` hello içinde `src\main\java\com\microsoft\example` dizin.</span><span class="sxs-lookup"><span data-stu-id="41a72-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="41a72-195">Metin olarak hello içeriği hello dosyaları için aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41a72-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="41a72-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="41a72-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="41a72-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="41a72-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a><span data-ttu-id="41a72-198">Merhaba topolojisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="41a72-198">Define hello topology</span></span>

<span data-ttu-id="41a72-199">Merhaba topolojisi hello spout'lar bağlar ve hello bileşenler arasında veri akışını tanımlayan bir grafik içine birlikte Cıvatalar.</span><span class="sxs-lookup"><span data-stu-id="41a72-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="41a72-200">Ayrıca, Storm hello bileşenleri hello küme içinde örneklerini oluştururken kullandığı paralellik ipuçlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="41a72-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="41a72-201">Merhaba aşağıdaki temel bir hello grafik bu topoloji bileşenleri diyagramı görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="41a72-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![Diyagram gösteren hello spout'lar ve düzenlemeyi Cıvatalar](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="41a72-203">tooimplement topoloji Merhaba, adlı bir dosya oluşturun `WordCountTopology.java` hello içinde `src\main\java\com\microsoft\example` dizin.</span><span class="sxs-lookup"><span data-stu-id="41a72-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="41a72-204">Java kod hello dosyasının Merhaba içeriğine aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="41a72-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="41a72-205">Günlük tutmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41a72-205">Configure logging</span></span>

<span data-ttu-id="41a72-206">Storm Apache Log4j toolog bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="41a72-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="41a72-207">Günlük kaydını yapılandırmazsanız hello topoloji tanılama bilgisi yayar.</span><span class="sxs-lookup"><span data-stu-id="41a72-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="41a72-208">ne kaydedilir, toocontrol adlı bir dosya oluşturun `log4j2.xml` hello içinde `resources` dizin.</span><span class="sxs-lookup"><span data-stu-id="41a72-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="41a72-209">XML hello hello dosyasının içeriğini aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="41a72-209">Use hello following XML as hello contents of hello file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="41a72-210">Yeni bir Günlükçü hello için bu XML yapılandırır `com.microsoft.example` Bu örnek topolojide hello bileşenleri içeren sınıf.</span><span class="sxs-lookup"><span data-stu-id="41a72-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="41a72-211">Merhaba düzeyi tootrace bu topolojide bileşenleri tarafından gösterilen tüm günlük bilgilerini yakalar bu Günlükçü için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="41a72-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="41a72-212">Merhaba `<Root level="error">` bölüm günlük hello kök düzeyi yapılandırır (içinde değil her şeyi `com.microsoft.example`) tooonly günlük hata bilgileri.</span><span class="sxs-lookup"><span data-stu-id="41a72-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="41a72-213">Log4j için günlüğe kaydetmeyi yapılandırma hakkında daha fazla bilgi için bkz: [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="41a72-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="41a72-214">Storm sürüm 0.10.0 ve daha yüksek kullanım Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="41a72-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="41a72-215">Storm eski sürümlerinde kullanılan Log4j günlük yapılandırması için farklı bir biçim kullanılan 1.x.</span><span class="sxs-lookup"><span data-stu-id="41a72-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="41a72-216">Merhaba eski yapılandırması hakkında daha fazla bilgi için bkz: [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="41a72-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="41a72-217">Yerel olarak test hello topolojisi</span><span class="sxs-lookup"><span data-stu-id="41a72-217">Test hello topology locally</span></span>

<span data-ttu-id="41a72-218">Merhaba dosyaları kaydettikten sonra yerel olarak komut tootest hello topolojisi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="41a72-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="41a72-219">Çalışırken, hello topolojisini başlangıç bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="41a72-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="41a72-220">Merhaba aşağıdaki metni hello word sayısı çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="41a72-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="41a72-221">Bu örnek günlük dosyası bu hello sözcüğü gösterir ' ve ' 113 kez yayılan.</span><span class="sxs-lookup"><span data-stu-id="41a72-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="41a72-222">Merhaba spout sürekli hello yayar çünkü hello topoloji çalıştığı sürece hello sayısı toogo yukarı devam aynı cümleleri.</span><span class="sxs-lookup"><span data-stu-id="41a72-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="41a72-223">Sözcükler yayımlanmasını ve sayılar arasında 5 saniye aralığını yoktur.</span><span class="sxs-lookup"><span data-stu-id="41a72-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="41a72-224">Merhaba **WordCount** bileşen yapılandırılmış değer çizgisi tanımlama grubu geldiğinde tooonly yayma bilgi.</span><span class="sxs-lookup"><span data-stu-id="41a72-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="41a72-225">Diziler yalnızca beş saniyede teslim edilir, onay ister.</span><span class="sxs-lookup"><span data-stu-id="41a72-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="41a72-226">Merhaba topoloji tooFlux Dönüştür</span><span class="sxs-lookup"><span data-stu-id="41a72-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="41a72-227">Flux uygulama tooseparate yapılandırmasından sağlayan bir yeni kullanılabilir Storm 0.10.0 veya üzeri bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="41a72-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="41a72-228">Bileşenlerinizi Java'da tanımlanmış olan ancak hello topoloji YAML dosyası kullanılarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="41a72-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="41a72-229">Projenizi ile varsayılan topoloji tanımı paketini veya tek başına dosya hello topoloji gönderirken kullanın.</span><span class="sxs-lookup"><span data-stu-id="41a72-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="41a72-230">Merhaba topoloji tooStorm gönderirken hello YAML topoloji tanımı ortam değişkenleri veya yapılandırma dosyaları toopopulate değerlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41a72-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="41a72-231">Merhaba YAML dosyası hello bileşenleri toouse hello topolojisi ve aralarındaki hello veri akışı için tanımlar.</span><span class="sxs-lookup"><span data-stu-id="41a72-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="41a72-232">Bir YAML dosyası hello jar dosyasını bir parçası olarak ekleyebilirsiniz veya dış YAML dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41a72-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="41a72-233">Flux hakkında daha fazla bilgi için bkz: [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="41a72-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="41a72-234">Son tooa [hata (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) Storm 1.0.1 tooinstall gerekebilir bir [Storm geliştirme ortamı](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux yerel olarak topolojileri.</span><span class="sxs-lookup"><span data-stu-id="41a72-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="41a72-235">Merhaba taşıma `WordCountTopology.java` dosya hello proje dışında.</span><span class="sxs-lookup"><span data-stu-id="41a72-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="41a72-236">Daha önce bu dosyayı hello topoloji tanımlı, ancak Flux ile gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="41a72-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="41a72-237">Merhaba, `resources` dizin adlı bir dosya oluşturun `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="41a72-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="41a72-238">Bu dosyanın içeriğini hello metin aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="41a72-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="41a72-239">Değişiklikleri toohello aşağıdaki hello olun `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="41a72-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="41a72-240">Yeni bağımlılık hello olarak aşağıdaki hello eklemek `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="41a72-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="41a72-241">Eklenti toohello aşağıdaki hello eklemek `<plugins>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="41a72-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="41a72-242">Bu eklenti hello proje için bir paket (jar dosyasını) hello oluşturulmasını işler ve bazı dönüşümleri belirli tooFlux hello paket oluştururken uygular.</span><span class="sxs-lookup"><span data-stu-id="41a72-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
                </transformers>
                <!-- Keep us from getting a bad signature error -->
                <filters>
                    <filter>
                        <artifact>*:*</artifact>
                        <excludes>
                            <exclude>META-INF/*.SF</exclude>
                            <exclude>META-INF/*.DSA</exclude>
                            <exclude>META-INF/*.RSA</exclude>
                        </excludes>
                    </filter>
                </filters>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        ```

   * <span data-ttu-id="41a72-243">Merhaba, **exec maven eklentisi** `<configuration>` bölümünde, hello değerini değiştirmek `<mainClass>` çok`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="41a72-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="41a72-244">Bu ayar hello topolojisi geliştirme yerel olarak çalışan Flux toohandle sağlar.</span><span class="sxs-lookup"><span data-stu-id="41a72-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="41a72-245">Merhaba, `<resources>` bölümünde, toohello aşağıdaki hello eklemek `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="41a72-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="41a72-246">Bu XML hello topoloji hello projesinin bir parçası tanımlayan hello YAML dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="41a72-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="41a72-247">Yerel olarak test hello flux topolojisi</span><span class="sxs-lookup"><span data-stu-id="41a72-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="41a72-248">Maven kullanarak hello Flux topolojisi yürütün ve toocompile aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="41a72-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="41a72-249">PowerShell kullanıyorsanız, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="41a72-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="41a72-250">Topolojiniz Storm 1.0.1 BITS kullanıyorsa, bu komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="41a72-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="41a72-251">Bu hatanın nedeni [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="41a72-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="41a72-252">Bunun yerine, [geliştirme ortamınızda Storm yüklemek](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) ve kullanım hello aşağıdaki bilgileri.</span><span class="sxs-lookup"><span data-stu-id="41a72-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="41a72-253">Varsa [Storm geliştirme ortamınızda yüklü](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), komutları bunun yerine aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="41a72-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="41a72-254">Merhaba `--local` parametre yerel modda hello topolojisi geliştirme ortamınızı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="41a72-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="41a72-255">Merhaba `-R /topology.yaml` parametresini kullanır hello `topology.yaml` hello jar dosyasını toodefine hello topoloji kaynak dosya.</span><span class="sxs-lookup"><span data-stu-id="41a72-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="41a72-256">Çalışırken, hello topolojisini başlangıç bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="41a72-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="41a72-257">metin aşağıdaki hello hello çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="41a72-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="41a72-258">Günlüğe kaydedilen bilgileri toplu işlemleri arasında 10 saniye gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="41a72-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="41a72-259">Merhaba kopyası `topology.yaml` hello proje dosyasından.</span><span class="sxs-lookup"><span data-stu-id="41a72-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="41a72-260">Ad hello yeni dosya `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="41a72-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="41a72-261">Merhaba, `newtopology.yaml` dosya, hello aşağıdaki bölümünde ve hello değerini değiştirme Bul `10` çok`5`.</span><span class="sxs-lookup"><span data-stu-id="41a72-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="41a72-262">Word'ün toplu yayma arasındaki bu değişikliği değişiklikleri hello aralığı 10 saniye too5 sayar.</span><span class="sxs-lookup"><span data-stu-id="41a72-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="41a72-263">Veya, geliştirme ortamınızı Storm varsa:</span><span class="sxs-lookup"><span data-stu-id="41a72-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="41a72-264">Değişiklik hello `/path/to/newtopology.yaml` hello önceki adımda oluşturduğunuz toohello yolu toohello newtopology.yaml dosyası.</span><span class="sxs-lookup"><span data-stu-id="41a72-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="41a72-265">Bu komut hello newtopology.yaml hello topoloji tanımı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="41a72-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="41a72-266">Biz hello eklemediniz beri `compile` parametresi, Maven önceki adımlarda kurulu hello proje hello sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="41a72-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="41a72-267">Bir kez hello topolojisini başlatır ve verilmiş toplu işlemleri arasındaki hello süre tooreflect hello newtopology.yaml değerinde değiştiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="41a72-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="41a72-268">Bu nedenle, yapılandırmanızı YAML dosyası aracılığıyla toorecompile hello topoloji gerek kalmadan değiştirebileceğiniz olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41a72-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="41a72-269">Bunlar ve diğer özellikler hello Flux framework'ün hakkında daha fazla bilgi için bkz: [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="41a72-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="41a72-270">Trident</span><span class="sxs-lookup"><span data-stu-id="41a72-270">Trident</span></span>

<span data-ttu-id="41a72-271">Trident Storm tarafından sağlanan üst düzey bir soyutlamadır.</span><span class="sxs-lookup"><span data-stu-id="41a72-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="41a72-272">Durum bilgisi olan işlemeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="41a72-272">It supports stateful processing.</span></span> <span data-ttu-id="41a72-273">Trident birincil avantajı Hello hello topoloji girer her ileti yalnızca bir kez işlenir garanti edebilir sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="41a72-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="41a72-274">Trident kullanmadan topolojinizi yalnızca iletileri en az bir kez işlenir garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="41a72-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="41a72-275">Cıvatalar oluşturmak yerine kullanılabilir yerleşik bileşenleri gibi diğer farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="41a72-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="41a72-276">Aslında, Cıvatalar filtreleri, tahminleri ve işlevleri gibi daha az genel bileşenler tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="41a72-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="41a72-277">Trident uygulamaları Maven projelerini kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="41a72-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="41a72-278">Hello kullandığınız aynı temel adımlar bu makalenin önceki bölümlerinde sunulan — yalnızca hello kodu farklı.</span><span class="sxs-lookup"><span data-stu-id="41a72-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="41a72-279">Trident de (şu anda) hello Flux framework ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="41a72-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="41a72-280">Trident hakkında daha fazla bilgi için bkz: Merhaba [Trident API genel bakış](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="41a72-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="41a72-281">Trident uygulama örneği için bkz: [hdınsight'ta Apache Storm oluşturan eğilim konuları Twitter](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="41a72-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41a72-282">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="41a72-282">Next Steps</span></span>

<span data-ttu-id="41a72-283">Öğrendiğiniz nasıl toocreate Java kullanarak bir Storm topolojisinin.</span><span class="sxs-lookup"><span data-stu-id="41a72-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="41a72-284">Daha fazla bilgi nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="41a72-284">Now learn how to:</span></span>

* [<span data-ttu-id="41a72-285">Dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="41a72-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="41a72-286">Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="41a72-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="41a72-287">Daha fazla örnek Storm topolojileri ziyaret ederek bulabileceğiniz [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="41a72-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

