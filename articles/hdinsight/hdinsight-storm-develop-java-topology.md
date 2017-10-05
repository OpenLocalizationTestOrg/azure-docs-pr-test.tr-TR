---
title: "Apache Storm örnek Java topolojisi - Azure Hdınsight | Microsoft Docs"
description: "Bir örnek word count topolojisi oluşturarak Java'da Apache Storm topolojilerini oluşturmayı öğrenin."
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
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="f12df-104">Apache Storm topolojisini Java oluşturma</span><span class="sxs-lookup"><span data-stu-id="f12df-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="f12df-105">Apache Storm için Java tabanlı bir topoloji oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f12df-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="f12df-106">Word-count uygulama uygulayan bir Storm topolojisinin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f12df-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="f12df-107">Maven oluşturun ve projeyi paketini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f12df-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="f12df-108">Ardından, nasıl Flux framework kullanarak topolojisi tanımlayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f12df-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="f12df-109">Flux Storm 0.10.0 veya sonraki sürümlerinde çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="f12df-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="f12df-110">Storm 0.10.0 Hdınsight 3.3 ve 3.4 ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f12df-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="f12df-111">Bu belgedeki adımları tamamladıktan sonra Hdınsight üzerinde Apache Storm topolojisini dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="f12df-112">Bu belgede oluşturulan Storm topolojisini örnekler tamamlanmış bir sürümünü şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="f12df-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f12df-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f12df-113">Prerequisites</span></span>

* [<span data-ttu-id="f12df-114">Java Geliştirme Seti (JDK) sürüm 7</span><span class="sxs-lookup"><span data-stu-id="f12df-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="f12df-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven Java projeleri için bir proje derleme sistemidir.</span><span class="sxs-lookup"><span data-stu-id="f12df-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="f12df-116">Bir metin düzenleyicisi veya IDE.</span><span class="sxs-lookup"><span data-stu-id="f12df-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="f12df-117">Ortam değişkenleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f12df-117">Configure environment variables</span></span>

<span data-ttu-id="f12df-118">Java ve JDK yüklediğinizde aşağıdaki ortam değişkenleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="f12df-119">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f12df-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="f12df-120">**JAVA_HOME** -Java Çalışma zamanı ortamı (JRE) yüklü olduğu dizine işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="f12df-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="f12df-121">Örneğin, bir UNIX veya Linux dağıtımlarında benzeri bir değer olması gereken `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="f12df-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="f12df-122">Windows'da benzeri bir değer gerekir`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="f12df-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="f12df-123">**YOL** -aşağıdaki yolları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="f12df-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="f12df-124">**JAVA_HOME** (veya eşdeğer yolu)</span><span class="sxs-lookup"><span data-stu-id="f12df-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="f12df-125">**JAVA_HOME\bin** (veya eşdeğer yolu)</span><span class="sxs-lookup"><span data-stu-id="f12df-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="f12df-126">Maven'ın yüklendiği dizin</span><span class="sxs-lookup"><span data-stu-id="f12df-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="f12df-127">Bir Maven projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="f12df-127">Create a Maven project</span></span>

<span data-ttu-id="f12df-128">Komut satırından adlı bir Maven projesi oluşturmak için aşağıdaki komutu kullanın. **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="f12df-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="f12df-129">PowerShell kullanıyorsanız, çevreleyen gerekir`-D` çift tırnak işareti parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="f12df-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="f12df-130">Bu komut adlı bir dizin oluşturur `WordCount` geçerli konumda içeren temel bir Maven projesi.</span><span class="sxs-lookup"><span data-stu-id="f12df-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="f12df-131">`WordCount` Dizini aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="f12df-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="f12df-132">`pom.xml`: Bir Maven projesi için ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="f12df-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="f12df-133">`src\main\java\com\microsoft\example`: Uygulama kodunuz içerir.</span><span class="sxs-lookup"><span data-stu-id="f12df-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="f12df-134">`src\test\java\com\microsoft\example`: Uygulamanız için testleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f12df-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="f12df-135">Oluşturulan örnek kodu Kaldır</span><span class="sxs-lookup"><span data-stu-id="f12df-135">Remove the generated example code</span></span>

<span data-ttu-id="f12df-136">Oluşturulan test ve uygulama dosyalarını silin:</span><span class="sxs-lookup"><span data-stu-id="f12df-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="f12df-137">**src\test\java\com\microsoft\example\AppTest.Java**</span><span class="sxs-lookup"><span data-stu-id="f12df-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="f12df-138">**src\main\java\com\microsoft\example\App.Java**</span><span class="sxs-lookup"><span data-stu-id="f12df-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="f12df-139">Maven depoları ekleme</span><span class="sxs-lookup"><span data-stu-id="f12df-139">Add Maven repositories</span></span>

<span data-ttu-id="f12df-140">Hdınsight Hortonworks veri Platformu (HDP) üzerinde dayalı, bu yüzden Apache Storm projelerinizi bağımlılıklarını karşıdan yüklemek için Hortonworks depo kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f12df-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="f12df-141">İçinde __pom.xml__ dosya, aşağıdaki XML'i ekleyin sonra `<url>http://maven.apache.org</url>` satır:</span><span class="sxs-lookup"><span data-stu-id="f12df-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="f12df-142">Özellikler ekleme</span><span class="sxs-lookup"><span data-stu-id="f12df-142">Add properties</span></span>

<span data-ttu-id="f12df-143">Maven özellikleri olarak adlandırılan proje düzeyi değerleri tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f12df-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="f12df-144">İçinde __pom.xml__, aşağıdaki metinden sonra Ekle `</repositories>` satır:</span><span class="sxs-lookup"><span data-stu-id="f12df-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="f12df-145">Bu değer diğer bölümlerinde artık kullanabilirsiniz `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="f12df-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="f12df-146">Örneğin, Storm bileşenleri belirtirken kullanabileceğiniz `${storm.version}` sabit bir değer kodlama yerine.</span><span class="sxs-lookup"><span data-stu-id="f12df-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="f12df-147">Bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f12df-147">Add dependencies</span></span>

<span data-ttu-id="f12df-148">Storm bileşenleri için bağımlılık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f12df-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="f12df-149">Açık `pom.xml` dosya ve aşağıdaki kodu ekleyin `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="f12df-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="f12df-150">Derleme zamanında Maven aramak için bu bilgileri kullanır `storm-core` Maven deposunda.</span><span class="sxs-lookup"><span data-stu-id="f12df-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="f12df-151">Yerel bilgisayarınızda depodaki İlk bakar.</span><span class="sxs-lookup"><span data-stu-id="f12df-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="f12df-152">Dosya yoksa, Maven ortak Maven depodan yükler ve yerel depoda depolar.</span><span class="sxs-lookup"><span data-stu-id="f12df-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="f12df-153">Bildirim `<scope>provided</scope>` bu bölümdeki satır.</span><span class="sxs-lookup"><span data-stu-id="f12df-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="f12df-154">Bu ayar dışlamak için Maven söyler **storm çekirdek** sistem tarafından sağlanan bulunduğundan, oluşturulan JAR dosyalarını.</span><span class="sxs-lookup"><span data-stu-id="f12df-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="f12df-155">Derleme yapılandırması</span><span class="sxs-lookup"><span data-stu-id="f12df-155">Build configuration</span></span>

<span data-ttu-id="f12df-156">Maven eklentileri projeyi derleme aşamaları özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f12df-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="f12df-157">Örneğin, projenin nasıl derlenmiş veya JAR dosyasına paketlemek nasıl.</span><span class="sxs-lookup"><span data-stu-id="f12df-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="f12df-158">Açık `pom.xml` dosya ve doğrudan yukarıdaki aşağıdaki kodu ekleyin `</project>` satır.</span><span class="sxs-lookup"><span data-stu-id="f12df-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="f12df-159">Bu bölümde, eklentiler, kaynakları ve diğer yapı yapılandırma seçeneklerini eklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f12df-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="f12df-160">Bir tam başvuru için **pom.xml** dosya için bkz: [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="f12df-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="f12df-161">Eklentiler</span><span class="sxs-lookup"><span data-stu-id="f12df-161">Add plug-ins</span></span>

<span data-ttu-id="f12df-162">Apache Storm topolojilerini Java'da, uygulanan için [Exec Maven eklentisi](http://www.mojohaus.org/exec-maven-plugin/) kolayca topolojisi geliştirme ortamınızı yerel olarak çalıştırmanızı izin verdiği için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f12df-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="f12df-163">Aşağıdakileri ekleyin `<plugins>` bölümünü `pom.xml` Exec Maven eklentisi eklenecek dosyası:</span><span class="sxs-lookup"><span data-stu-id="f12df-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

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

<span data-ttu-id="f12df-164">Başka bir eklenti yararlı [Apache Maven derleyici eklentisi](http://maven.apache.org/plugins/maven-compiler-plugin/), derleme seçeneklerini değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f12df-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="f12df-165">Java değişiklikleri kaynak ve hedef uygulamanız için Maven kullanımları sürümü.</span><span class="sxs-lookup"><span data-stu-id="f12df-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="f12df-166">Hdınsight için __3.4 veya önceki__, kaynak ayarlayabilir ve Java sürümü için hedef __1.7__.</span><span class="sxs-lookup"><span data-stu-id="f12df-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="f12df-167">Hdınsight için __3.5__, kaynak ayarlayabilir ve Java sürümü için hedef __1.8__.</span><span class="sxs-lookup"><span data-stu-id="f12df-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="f12df-168">Aşağıdaki metni eklemek `<plugins>` bölümünü `pom.xml` Apache Maven derleyici eklentisi eklenecek dosyası.</span><span class="sxs-lookup"><span data-stu-id="f12df-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="f12df-169">Hedef Hdınsight sürüm 3.5 olması için bu örnek 1.8, belirtir.</span><span class="sxs-lookup"><span data-stu-id="f12df-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="f12df-170">Kaynaklarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f12df-170">Configure resources</span></span>

<span data-ttu-id="f12df-171">Kaynakları bölümü kod olmayan kaynakları topolojideki bileşenleri tarafından gereken yapılandırma dosyaları gibi eklemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f12df-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="f12df-172">Bu örnek için aşağıdaki metni eklemek `<resources>` bölümünü ' pom.xml dosyasını.</span><span class="sxs-lookup"><span data-stu-id="f12df-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="f12df-173">Bu örnek kaynaklar directory proje kök dizininde ekler (`${basedir}`) kaynaklar içeriyor ve adlı dosyayı içeren bir konum olarak `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="f12df-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="f12df-174">Bu dosya, hangi bilgilerin topolojisi tarafından kaydedilir yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f12df-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="f12df-175">Topoloji oluşturma</span><span class="sxs-lookup"><span data-stu-id="f12df-175">Create the topology</span></span>

<span data-ttu-id="f12df-176">Java tabanlı Apache Storm topolojisini bağımlılık olarak yazmanız gerekir üç bileşeni (veya başvuru) oluşur.</span><span class="sxs-lookup"><span data-stu-id="f12df-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="f12df-177">**Spout'lar**: dış veri kaynakları ve veri akışları topoloji yayar okur.</span><span class="sxs-lookup"><span data-stu-id="f12df-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="f12df-178">**Cıvatalar**: spout'lar veya diğer Cıvatalar tarafından gösterilen akışları üzerinde işlemeyi gerçekleştirir ve bir veya daha fazla akışları yayar.</span><span class="sxs-lookup"><span data-stu-id="f12df-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="f12df-179">**Topoloji**: nasıl spout'lar Cıvatalar düzenlenir ve giriş noktası için topoloji sunar tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f12df-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="f12df-180">Spout oluşturma</span><span class="sxs-lookup"><span data-stu-id="f12df-180">Create the spout</span></span>

<span data-ttu-id="f12df-181">Dış veri kaynakları için gereksinimler azaltmak için aşağıdaki spout yalnızca rastgele cümleleri yayar.</span><span class="sxs-lookup"><span data-stu-id="f12df-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="f12df-182">İle sağlanan bir spout değiştirilmiş bir sürümünü olan [Storm Starter örnekleri](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="f12df-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="f12df-183">Bir dış veri kaynağından okur spout bir örnek için aşağıdaki örneklerde birine bakın:</span><span class="sxs-lookup"><span data-stu-id="f12df-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="f12df-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): Twitter'dan okuyan bir örnek spout</span><span class="sxs-lookup"><span data-stu-id="f12df-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="f12df-185">[Storm Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): Kafka okur spout</span><span class="sxs-lookup"><span data-stu-id="f12df-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="f12df-186">Spout için adlı bir dosya oluşturun `RandomSentenceSpout.java` içinde `src\main\java\com\microsoft\example` dizin ve kullanım aşağıdaki Java kod içeriği:</span><span class="sxs-lookup"><span data-stu-id="f12df-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

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
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
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

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="f12df-187">Bu topoloji yalnızca bir spout kullansa da, diğerlerinin birkaç topoloji farklı kaynaklardan veri akışı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f12df-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="f12df-188">Cıvatalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="f12df-188">Create the bolts</span></span>

<span data-ttu-id="f12df-189">Cıvatalar veri işleme işleyin.</span><span class="sxs-lookup"><span data-stu-id="f12df-189">Bolts handle the data processing.</span></span> <span data-ttu-id="f12df-190">Bu topoloji iki Cıvatalar kullanır:</span><span class="sxs-lookup"><span data-stu-id="f12df-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="f12df-191">**SplitSentence**: tarafından gösterilen cümleleri böler **RandomSentenceSpout** ayrı sözcükleri içine.</span><span class="sxs-lookup"><span data-stu-id="f12df-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="f12df-192">**WordCount**: her sözcüğün oluştu kaç kez sayar.</span><span class="sxs-lookup"><span data-stu-id="f12df-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="f12df-193">Cıvatalar hiçbir şey, örneğin, hesaplama, sürdürme veya dış bileşenlere Konuşmayı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="f12df-194">İki yeni dosyalar oluşturma `SplitSentence.java` ve `WordCount.java` içinde `src\main\java\com\microsoft\example` dizin.</span><span class="sxs-lookup"><span data-stu-id="f12df-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="f12df-195">Aşağıdaki metin dosyalarını içeriği kullanın:</span><span class="sxs-lookup"><span data-stu-id="f12df-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="f12df-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="f12df-196">SplitSentence</span></span>

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

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
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

#### <a name="wordcount"></a><span data-ttu-id="f12df-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="f12df-197">WordCount</span></span>

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
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
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
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
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

### <a name="define-the-topology"></a><span data-ttu-id="f12df-198">Topolojisi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="f12df-198">Define the topology</span></span>

<span data-ttu-id="f12df-199">Spout'lar bağlar ve bileşenler arasında veri akışını tanımlayan bir grafik içine birlikte Cıvatalar topoloji.</span><span class="sxs-lookup"><span data-stu-id="f12df-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="f12df-200">Ayrıca, Storm bileşenleri kümedeki örneklerini oluştururken kullandığı paralellik ipuçlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f12df-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="f12df-201">Aşağıdaki resimde, grafik bileşenlerinin bu topoloji için temel bir diyagramıdır.</span><span class="sxs-lookup"><span data-stu-id="f12df-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![spout'lar ve Cıvatalar düzenlemesini gösteren diyagram](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="f12df-203">Topoloji uygulamak için adlı bir dosya oluşturun `WordCountTopology.java` içinde `src\main\java\com\microsoft\example` dizin.</span><span class="sxs-lookup"><span data-stu-id="f12df-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="f12df-204">Aşağıdaki Java kod dosyasının içeriği kullanın:</span><span class="sxs-lookup"><span data-stu-id="f12df-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="f12df-205">Günlük tutmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f12df-205">Configure logging</span></span>

<span data-ttu-id="f12df-206">Storm bilgileri günlüğe kaydetmek için Apache Log4j kullanır.</span><span class="sxs-lookup"><span data-stu-id="f12df-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="f12df-207">Günlük kaydını yapılandırmazsanız topoloji tanılama bilgisi yayar.</span><span class="sxs-lookup"><span data-stu-id="f12df-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="f12df-208">Günlüğe kaydedilenler denetlemek için adlı bir dosya oluşturun `log4j2.xml` içinde `resources` dizin.</span><span class="sxs-lookup"><span data-stu-id="f12df-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="f12df-209">Aşağıdaki XML dosyasının içeriği kullanın.</span><span class="sxs-lookup"><span data-stu-id="f12df-209">Use the following XML as the contents of the file.</span></span>

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

<span data-ttu-id="f12df-210">Yeni bir Günlükçü için bu XML yapılandırır `com.microsoft.example` Bu örnek topolojide bileşenlerini içeren sınıf.</span><span class="sxs-lookup"><span data-stu-id="f12df-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="f12df-211">Düzeyi izleme bu topolojide bileşenleri tarafından gösterilen tüm günlük bilgilerini yakalar bu Günlükçü için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f12df-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="f12df-212">`<Root level="error">` Bölümü kök düzeyini yapılandırır (içinde değil her şeyi `com.microsoft.example`) yalnızca hata bilgileri günlüğe kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="f12df-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="f12df-213">Log4j için günlüğe kaydetmeyi yapılandırma hakkında daha fazla bilgi için bkz: [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="f12df-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="f12df-214">Storm sürüm 0.10.0 ve daha yüksek kullanım Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="f12df-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="f12df-215">Storm eski sürümlerinde kullanılan Log4j günlük yapılandırması için farklı bir biçim kullanılan 1.x.</span><span class="sxs-lookup"><span data-stu-id="f12df-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="f12df-216">Eski yapılandırma hakkında daha fazla bilgi için bkz: [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="f12df-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="f12df-217">Topoloji yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="f12df-217">Test the topology locally</span></span>

<span data-ttu-id="f12df-218">Dosyaları kaydettikten sonra topoloji yerel olarak test etmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f12df-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="f12df-219">Çalışırken, topoloji başlangıç bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f12df-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="f12df-220">Aşağıdaki metni word sayısı çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="f12df-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="f12df-221">Bu örnek günlük belirten word 've' 113 kez yayılan.</span><span class="sxs-lookup"><span data-stu-id="f12df-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="f12df-222">Sayı spout sürekli olarak aynı cümleleri yayar çünkü topoloji çalıştığı sürece gidebilir devam eder.</span><span class="sxs-lookup"><span data-stu-id="f12df-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="f12df-223">Sözcükler yayımlanmasını ve sayılar arasında 5 saniye aralığını yoktur.</span><span class="sxs-lookup"><span data-stu-id="f12df-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="f12df-224">**WordCount** bileşen değer çizgisi tanımlama grubu geldiğinde bilgileri yalnızca yaymak üzere yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="f12df-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="f12df-225">Diziler yalnızca beş saniyede teslim edilir, onay ister.</span><span class="sxs-lookup"><span data-stu-id="f12df-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="f12df-226">Topoloji Flux için Dönüştür</span><span class="sxs-lookup"><span data-stu-id="f12df-226">Convert the topology to Flux</span></span>

<span data-ttu-id="f12df-227">Flux, uygulama yapılandırmasından ayırmanıza olanak sağlayan bir yeni kullanılabilir Storm 0.10.0 veya üzeri bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="f12df-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="f12df-228">Bileşenlerinizi Java'da tanımlanmış olan ancak topoloji YAML dosyası kullanılarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f12df-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="f12df-229">Projenizi ile varsayılan topoloji tanımı paketini veya tek başına dosya topoloji gönderirken kullanın.</span><span class="sxs-lookup"><span data-stu-id="f12df-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="f12df-230">Storm için topoloji gönderirken YAML topoloji tanımı değerleri doldurmak için ortam değişkenleri veya yapılandırma dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="f12df-231">Topoloji ve verileri için kullanılacak bileşenleri YAML dosyası tanımlar aralarında akış.</span><span class="sxs-lookup"><span data-stu-id="f12df-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="f12df-232">Bir YAML dosyası jar dosyasını bir parçası olarak ekleyebilirsiniz veya dış YAML dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="f12df-233">Flux hakkında daha fazla bilgi için bkz: [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f12df-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="f12df-234">Verilecek bir [hata (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) Storm 1.0.1 yüklemeniz gerekebilir bir [Storm geliştirme ortamı](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) Flux topolojileri yerel olarak çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="f12df-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="f12df-235">Taşıma `WordCountTopology.java` dosya proje dışında.</span><span class="sxs-lookup"><span data-stu-id="f12df-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="f12df-236">Daha önce bu dosyayı topoloji tanımlı, ancak Flux ile gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f12df-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="f12df-237">İçinde `resources` dizin adlı bir dosya oluşturun `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f12df-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="f12df-238">Aşağıdaki metni bu dosyanın içeriğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f12df-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
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
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="f12df-239">Aşağıdaki değişiklikleri yapın `pom.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="f12df-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="f12df-240">Aşağıdaki yeni bağımlılık olarak ekleme `<dependencies>` bölümü:</span><span class="sxs-lookup"><span data-stu-id="f12df-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="f12df-241">Aşağıdaki eklenti ekleme `<plugins>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="f12df-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="f12df-242">Bu eklenti projesi için bir paket (jar dosyasını) oluşturulmasını işler ve belirli bazı dönüşümleri paket oluştururken Flux için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f12df-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
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
                    <!-- We're using Flux, so refer to it as main -->
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

   * <span data-ttu-id="f12df-243">İçinde **exec maven eklentisi** `<configuration>` bölümünde, değerini değiştirin `<mainClass>` için `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="f12df-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="f12df-244">Bu ayar topolojisi geliştirme yerel olarak çalışan işlemeye Flux sağlar.</span><span class="sxs-lookup"><span data-stu-id="f12df-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="f12df-245">İçinde `<resources>` bölümünde, aşağıdakileri ekleyin `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="f12df-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="f12df-246">Bu XML topoloji projenin bir parçası tanımlayan YAML dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="f12df-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="f12df-247">Flux topoloji yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="f12df-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="f12df-248">Maven kullanarak Flux topolojisi derleyip için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="f12df-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="f12df-249">PowerShell kullanıyorsanız, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f12df-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="f12df-250">Topolojiniz Storm 1.0.1 BITS kullanıyorsa, bu komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f12df-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="f12df-251">Bu hatanın nedeni [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="f12df-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="f12df-252">Bunun yerine, [geliştirme ortamınızda Storm yüklemek](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) ve aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f12df-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="f12df-253">Varsa [Storm geliştirme ortamınızda yüklü](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), bunun yerine aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f12df-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="f12df-254">`--local` Parametre yerel modda topolojisi geliştirme ortamınızı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f12df-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="f12df-255">`-R /topology.yaml` Parametresini kullanır `topology.yaml` topoloji tanımlamak için jar dosyasından kaynak dosya.</span><span class="sxs-lookup"><span data-stu-id="f12df-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="f12df-256">Çalışırken, topoloji başlangıç bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f12df-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="f12df-257">Aşağıdaki metni çıkış örneğidir:</span><span class="sxs-lookup"><span data-stu-id="f12df-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="f12df-258">Günlüğe kaydedilen bilgileri toplu işlemleri arasında 10 saniye gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="f12df-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="f12df-259">Bir kopyasını `topology.yaml` proje dosyasından.</span><span class="sxs-lookup"><span data-stu-id="f12df-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="f12df-260">Yeni dosya adı `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f12df-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="f12df-261">İçinde `newtopology.yaml` dosya, aşağıdaki bölümü bulun ve değerini değiştirme `10` için `5`.</span><span class="sxs-lookup"><span data-stu-id="f12df-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="f12df-262">Bu değişikliği 5 için 10 saniye gelen sözcük sayıları verme toplu arasındaki aralığı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f12df-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="f12df-263">Veya, geliştirme ortamınızı Storm varsa:</span><span class="sxs-lookup"><span data-stu-id="f12df-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="f12df-264">Değişiklik `/path/to/newtopology.yaml` önceki adımda oluşturduğunuz newtopology.yaml dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="f12df-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="f12df-265">Bu komut newtopology.yaml topoloji tanımı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="f12df-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="f12df-266">Biz eklemediniz beri `compile` parametresi, Maven, önceki adımda yapılandırdığınız projenin sürümü kullanır.</span><span class="sxs-lookup"><span data-stu-id="f12df-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="f12df-267">Topoloji başladıktan sonra verilmiş toplu işlemleri arasındaki süre newtopology.yaml değerinde yansıtmak üzere değiştirilmiştir dikkat etmelidir.</span><span class="sxs-lookup"><span data-stu-id="f12df-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="f12df-268">Bu nedenle, yapılandırmanızı YAML dosyası aracılığıyla topoloji yeniden derlemenize gerek kalmadan değiştirebileceğiniz olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="f12df-269">Bunlar ve diğer özellikler Flux framework'ün hakkında daha fazla bilgi için bkz: [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="f12df-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="f12df-270">Trident</span><span class="sxs-lookup"><span data-stu-id="f12df-270">Trident</span></span>

<span data-ttu-id="f12df-271">Trident Storm tarafından sağlanan üst düzey bir soyutlamadır.</span><span class="sxs-lookup"><span data-stu-id="f12df-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="f12df-272">Durum bilgisi olan işlemeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="f12df-272">It supports stateful processing.</span></span> <span data-ttu-id="f12df-273">Trident birincil avantajı, topoloji girer her ileti yalnızca bir kez işlenir garanti edebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="f12df-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="f12df-274">Trident kullanmadan topolojinizi yalnızca iletileri en az bir kez işlenir garanti edebilir.</span><span class="sxs-lookup"><span data-stu-id="f12df-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="f12df-275">Cıvatalar oluşturmak yerine kullanılabilir yerleşik bileşenleri gibi diğer farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="f12df-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="f12df-276">Aslında, Cıvatalar filtreleri, tahminleri ve işlevleri gibi daha az genel bileşenler tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="f12df-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="f12df-277">Trident uygulamaları Maven projelerini kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f12df-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="f12df-278">Aynı temel adımlar bu makalenin önceki bölümlerinde sunulan gibi kullandığınız — yalnızca kodu farklı.</span><span class="sxs-lookup"><span data-stu-id="f12df-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="f12df-279">Trident de (şu anda) Flux framework ile kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f12df-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="f12df-280">Trident hakkında daha fazla bilgi için bkz: [Trident API genel bakış](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="f12df-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="f12df-281">Trident uygulama örneği için bkz: [hdınsight'ta Apache Storm oluşturan eğilim konuları Twitter](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="f12df-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f12df-282">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f12df-282">Next Steps</span></span>

<span data-ttu-id="f12df-283">Java kullanarak bir Storm topolojisinin oluşturma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="f12df-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="f12df-284">Daha fazla bilgi nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="f12df-284">Now learn how to:</span></span>

* [<span data-ttu-id="f12df-285">Dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="f12df-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="f12df-286">Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="f12df-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="f12df-287">Daha fazla örnek Storm topolojileri ziyaret ederek bulabileceğiniz [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f12df-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

