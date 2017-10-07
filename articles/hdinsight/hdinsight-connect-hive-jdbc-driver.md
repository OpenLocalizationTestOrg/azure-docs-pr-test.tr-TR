---
title: "Merhaba JDBC sürücüsü - Azure Hdınsight ile Hive aaaQuery | Microsoft Docs"
description: "Hdınsight'ta bir Java uygulaması toosubmit Hive sorguları tooHadoop gelen Hello JDBC sürücüsü kullanın. Program aracılığıyla ve hello SQuirrel SQL istemciden bağlanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Hdınsight'ta hello JDBC sürücüsü aracılığıyla Hive sorgusu

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Java uygulama toosubmit Hive toouse hello JDBC sürücüsünden tooHadoop Azure hdınsight'ta nasıl sorgular öğrenin. Bu belgedeki Hello bilgiler gösterilmektedir nasıl tooconnect program aracılığıyla ve hello SQuirrel SQL istemci.

Merhaba Hive JDBC arabirimi hakkında daha fazla bilgi için bkz: [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight kümesi Hadoop'ta. Linux tabanlı veya Windows tabanlı kümeler çalışır.

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight 3.3 devre dışı bırakma](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL JDBC istemci uygulamasıdır.

* Merhaba [Java Geliştirme Seti (JDK) sürüm 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek.

* [Apache Maven](https://maven.apache.org). Maven bir projeyi derleme bu makaleyle ilişkili hello projesi tarafından kullanılan sistem Java projeleri için ' dir.

## <a name="jdbc-connection-string"></a>JDBC bağlantı dizesi

JDBC bağlantıları tooan Hdınsight kümesine Azure üzerinde 443 yapılır ve hello trafiği güvenliğinin SSL ile. arkasında hello kümeleri sit hello arası ortak ağ geçidi HiveServer2 gerçekten dinlediği hello trafiği toohello bağlantı noktası yönlendirir. Merhaba, bir örnek bağlantı dizesi aşağıdadır:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Değiştir `CLUSTERNAME` Hdınsight kümenize hello adı.

## <a name="authentication"></a>Kimlik Doğrulaması

Merhaba bağlantı kurulurken hello Hdınsight Küme Yönetici adı ve parola tooauthenticate toohello küme ağ geçidi kullanmanız gerekir. SQuirreL SQL gibi JDBC istemcilerinden bağlanırken istemci ayarları'nda hello yönetici adı ve parola girmeniz gerekir.

Bir Java uygulamasında bir bağlantı kurulurken hello adını ve parolasını kullanmanız gerekir. Örneğin, hello aşağıdaki Java kod hello bağlantı dizesi, yönetici adı ve parola kullanarak yeni bir bağlantı açar:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>SQuirreL SQL istemci ile bağlanma

SQuirreL SQL çalıştırmak kullanılan tooremotely Hive sorguları Hdınsight kümenize ile olabilecek bir JDBC istemcidir. Merhaba aşağıdaki adımlarda SQuirreL SQL zaten yüklemiş olduğunuz varsayılmaktadır.

1. Merhaba Hive JDBC sürücülerini Hdınsight kümenize kopyalayın.

    * İçin **Linux tabanlı Hdınsight**, kullanım hello aşağıdaki adımları toodownload gerekli hello jar dosyalarını.

        1. Merhaba dosyaları içeren bir dizin oluşturun. Örneğin, `mkdir hivedriver`.

        2. Bir komut satırından toocopy hello hello Hdınsight kümesi dosyalarından kullanım hello aşağıdaki komutlar:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Değiştir `USERNAME` hello küme için hello SSH kullanıcı hesabı adı ile. Değiştir `CLUSTERNAME` hello Hdınsight küme adı ile.

    * İçin **Windows tabanlı Hdınsight**, kullanım hello aşağıdaki adımları toodownload hello jar dosyalarını.

        1. Hello Azure portal, Hdınsight kümenize seçin ve ardından hello seçin **Uzak Masaüstü** simgesi.

            ![Uzak Masaüstü simgesi](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Merhaba Uzak Masaüstü dikey penceresinde hello kullan **Bağlan** düğmesini tooconnect toohello küme. Hello Uzak Masaüstü etkin değilse hello form tooprovide bir kullanıcı adı ve parolayı kullanın ve ardından **etkinleştirmek** hello kümesi için Uzak Masaüstü tooenable.

            ![Uzak Masaüstü dikey penceresi](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Seçtikten sonra **Bağlan**, bir .rdp dosyası indirilir. Bu dosya toolaunch hello uzak masaüstü istemcisini kullanın. İstendiğinde, hello kullanıcı adını ve Uzak Masaüstü erişimi için girdiğiniz parola kullanın.

        3. Bağlantı kurulduktan sonra hello hello Uzak Masaüstü oturumu tooyour yerel makineden aşağıdaki dosyaları kopyalayın. Adlı yerel bir dizinde put `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-JDBC-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > hello sürüm numaraları Hello yollarını ve dosya adlarını dahil, kümeniz için farklı olabilir.

        4. Merhaba dosyaları kopyalanıyor tamamladıktan sonra hello Uzak Masaüstü oturumu bağlantısını kesin.

2. Merhaba SQuirreL SQL uygulaması başlatın. Merhaba penceresinde Hello soldan seçin **sürücüleri**.

    ![Merhaba penceresinin sol tarafındaki hello sürücüler sekmesinde](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Merhaba simgeler hello hello üstündeki gelen **sürücüleri** iletişim, select hello  **+**  simgesi toocreate bir sürücü.

    ![Sürücüleri simgeler](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. Merhaba sürücü Ekle iletişim kutusunda, aşağıdaki bilgilerle hello ekleyin:

    * **Ad**: yığını
    * **Örnek URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Ek sınıf yolu**: indirilen kullanım hello Ekle düğmesi tooadd hello jar dosyaları daha önce
    * **Sınıf adı**: org.apache.hive.jdbc.HiveDriver

   ![sürücü iletişim ekleyin](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Tıklatın **Tamam** toosave bu ayarlar.

5. Merhaba SQuirreL SQL penceresinde Hello solda seçin **diğer adlar**. Merhaba ardından  **+**  simgesi toocreate bir bağlantı diğer adı.

    ![Yeni diğer ad ekleyin](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Kullanım hello aşağıdaki değerleri Merhaba **diğer ad eklemek** iletişim.

    * **Ad**: Hdınsight'ta Hive

    * **Sürücü**: kullanım hello açılır tooselect hello **Hive** sürücüsü

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Değiştir **CLUSTERNAME** Hdınsight kümenize hello adı.

    * **Kullanıcı adı**: Hdınsight kümenizin hello küme oturum açma hesabı adı. Merhaba varsayılan `admin`.

    * **Parola**: hello hello küme oturum açma hesabının parolasını.

 ![diğer iletişim ekleyin](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Kullanım hello **Test** bağlantı works hello düğmesi tooverify. Zaman **bağlanın: Hdınsight'ta Hive** seçin iletişim kutusu görüntülenirse, **Bağlan** tooperform hello test. Gördüğünüz Hello testi başarılı olursa bir **bağlantı başarılı** iletişim.

    toosave hello bağlantısı diğer adı hello kullan **Tamam** düğmesi hello hello sonundaki **diğer ad eklemek** iletişim.

7. Merhaba gelen **bağlanmak** SQuirreL SQL hello üstündeki açılan seçin **Hdınsight'ta Hive**. İstendiğinde, seçin **Bağlan**.

    ![Bağlantı iletişim kutusu](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Bağlantı kurulduktan sonra aşağıdaki sorgu hello SQL sorgusu iletişim kutusuna ve ardından hello seçin hello girin **çalıştırmak** simgesi. Hello sonuçları alanı hello hello sorgunun sonuçlarını göstermesi gerekir.

        select * from hivesampletable limit 10;

    ![Sonuçları dahil olmak üzere sql sorgu iletişim kutusu](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Bir örnek Java uygulaması Bağlan

Java istemci tooquery Hive kullanarak bir örnek kullanılabilir [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Merhaba depo toobuild Hello yönergeleri izleyin ve hello örnek çalıştırın.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Çalışırken tooopen SQL Bağlantısı beklenmeyen bir hata oluştu

**Belirtiler**: sürüm 3.3 veya 3.4 tooan Hdınsight kümesi bağlanırken beklenmeyen bir hata oluştu hata alabilirsiniz. Bu hata Hello yığın izlemesi satırlardan hello ile başlar:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Neden**: Bu hata SQuirreL ve hello bir hello Hive JDBC bileşenleri tarafından zorunlu tarafından kullanılan hello commons codec.jar dosyası hello sürümündeki bir uyuşmazlık kaynaklanır.

**Çözümleme**: Bu hata, kullanım hello aşağıdaki adımları toofix:

1. Hdınsight kümenize Hello commons codec jar dosyasını indirin.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. SQuirreL çıkın ve ardından SQuirreL, sisteminizde yüklü olduğu toohello dizinine gidin. Merhaba altındaki hello SquirreL dizininde `lib` dizini Değiştir hello varolan commons-codec.jar bir indirilen hello Hdınsight kümeden hello ile.

3. SQuirreL yeniden başlatın. Merhaba hata artık hdınsight'ta tooHive bağlanırken olmalıdır.

## <a name="next-steps"></a>Sonraki adımlar

Göre nasıl toouse JDBC toowork Hive, aşağıdaki kullanım hello ile diğer yolları toowork Azure Hdınsight ile tooexplore bağlar öğrendiniz.

* [Veri tooHDInsight karşıya yükle](hdinsight-upload-data.md)
* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [HDInsight ile MapReduce işleri kullanma](hdinsight-use-mapreduce.md)
