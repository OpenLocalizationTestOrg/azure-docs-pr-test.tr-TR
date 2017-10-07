---
title: "aaaJava kullanıcı tanımlı işlev (UDF hdınsight'ta - Azure Hive ile) | Microsoft Docs"
description: "Öğrenin nasıl toocreate Java tabanlı kullanıcı tanımlı işlev (UDF), Hive ile çalışır. Bu örnek UDF metin dizelerini toolowercase tablosu dönüştürür."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Bir Java kullanma UDF hdınsight'ta Hive ile

Öğrenin nasıl toocreate Java tabanlı kullanıcı tanımlı işlev (UDF), Hive ile çalışır. Bu örnekte Hello Java UDF metin dizelerini tooall küçük karakterden oluşan bir tablo dönüştürür.

## <a name="requirements"></a>Gereksinimler

* Hdınsight kümesi 

    > [!IMPORTANT]
    > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

    Bu belgedeki çoğu adımlar her iki Windows ve Linux tabanlı kümelerde çalışır. Ancak, hello kullanılan adımları tooupload hello UDF toohello küme ve belirli tooLinux tabanlı kümeler olan Çalıştır derlenmiş. Windows tabanlı kümeler ile kullanılabilir tooinformation bağlantılar sağlanmaktadır.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 veya sonraki (veya eşdeğeri, OpenJDK gibi bir)

* [Apache Maven](http://maven.apache.org/)

* Bir metin düzenleyicisi veya Java IDE

    > [!IMPORTANT]
    > Windows İstemcisi Python dosyalarda hello oluşturursanız, LF satır bitiş olarak kullanan bir Düzenleyicisi'ni kullanmanız gerekir. Merhaba düzenleyicinizi LF veya CRLF kullanıp kullanmadığını emin değilseniz bkz [sorun giderme](#troubleshooting) CR karakteri kaldırma adımları hello için bölüm.

## <a name="create-an-example-java-udf"></a>Java UDF örnek oluşturma 

1. Bir komut satırından toocreate yeni bir Maven projesi aşağıdaki hello kullan:

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > PowerShell kullanıyorsanız, hello parametreleri tırnak konulmalıdır. Örneğin, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Bu komut adlı bir dizin oluşturur **exampleudf**, hello Maven projesine içerir.

2. Merhaba Proje oluşturulduktan sonra hello silme **exampleudf/src/test** hello projesinin bir parçası oluşturulan dizini.

3. Açık hello **exampleudf/pom.xml**ve hello varolan `<dependencies>` XML aşağıdaki hello girişle:

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    Bu girişler Hadoop ve Hdınsight 3.5 ile birlikte dahil Hive hello sürümünü belirtin. Hadoop ve Hdınsight ile hello sağlanan Hive hello sürümleri hakkında bilgi bulabilirsiniz [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md) belge.

    Ekleme bir `<build>` hello önce bölümdeki `</project>` hello hello dosyasının sonuna satırında. Bu bölümde, XML aşağıdaki hello içermelidir:

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
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
        </plugins>
    </build>
    ```

    Bu girişler nasıl toobuild hello proje tanımlayın. Özellikle, hello sürümü proje kullanır hello Java ve nasıl toobuild dağıtım toohello küme için bir uberjar.

    Merhaba değişiklikler yapıldıktan sonra hello dosyasını kaydedin.

4. Yeniden Adlandır **exampleudf/src/main/java/com/microsoft/examples/App.java** çok**ExampleUDF.java**ve düzenleyicinizde hello dosyasını açın.

5. Merhaba Hello içeriğini değiştirin **ExampleUDF.java** dosya hello aşağıdakilerle sonra hello dosyasını kaydedin.

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    Bu kod bir dize değeri kabul eder ve hello dizeyi küçük harfli sürümünü döndüren bir UDF uygular.

## <a name="build-and-install-hello-udf"></a>Derleme ve hello UDF yükleyin

1. Merhaba UDF paketini ve komut toocompile aşağıdaki hello kullanın:

    ```bash
    mvn compile package
    ```

    Bu komut oluşturur ve paket hello UDF hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` dosya.

2. Kullanım hello `scp` komutu toocopy hello dosya toohello Hdınsight kümesi.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Değiştir `myuser` hello kümeniz için SSH kullanıcı hesabı ile. Değiştir `mycluster` hello küme adı ile. Bir parola toosecure hello SSH hesabı kullandıysanız, istendiğinde tooenter hello parola olur. Bir sertifika kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello özel anahtar dosyası.

3. SSH kullanarak toohello kümesine bağlanın.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

4. Merhaba SSH oturumundan hello jar dosyasını tooHDInsight depolama kopyalayın.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Merhaba UDF kovanından kullanın

1. Toostart hello Beeline istemci hello SSH oturumundan aşağıdaki hello kullanın.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Bu komut hello varsayılan kullanılan varsayar **yönetici** hello oturum açma hesabı kümeniz için.

2. Hello gelmesini sonra `jdbc:hive2://localhost:10001/>` sor, tooadd hello UDF tooHive aşağıdaki hello girin ve bir işlevi olarak kullanıma sunar.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > Bu örnek, Azure Storage hello kümesi için varsayılan depolama olduğunu varsayar. Bunun yerine, küme Data Lake Store kullanıyorsa, hello değiştirmek `wasb:///` çok değer`adl:///`.

3. Tablo toolower servis talebi dizelerden alınan hello UDF tooconvert değerlerini kullanın.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    Merhaba tablosundan cihaz Platformu (Android, Windows, iOS, vb.) seçer hello bu sorgu, hello dize toolower durumda dönüştürmek ve bunları görüntüler. Merhaba çıktı metin aşağıdaki benzer toohello görünür:

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a>Sonraki adımlar

Hive ile diğer yolları toowork için bkz: [Hdınsight ile Hive kullanma](hdinsight-use-hive.md).

Hive User-Defined işlevler hakkında daha fazla bilgi için bkz: [Hive işleçler ve kullanıcı tanımlı işlevler](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) hello Hive wiki Apache.org bölümü.
