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
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="c1e5f-104">Hdınsight'ta hello JDBC sürücüsü aracılığıyla Hive sorgusu</span><span class="sxs-lookup"><span data-stu-id="c1e5f-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="c1e5f-105">Java uygulama toosubmit Hive toouse hello JDBC sürücüsünden tooHadoop Azure hdınsight'ta nasıl sorgular öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="c1e5f-106">Bu belgedeki Hello bilgiler gösterilmektedir nasıl tooconnect program aracılığıyla ve hello SQuirrel SQL istemci.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="c1e5f-107">Merhaba Hive JDBC arabirimi hakkında daha fazla bilgi için bkz: [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="c1e5f-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1e5f-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c1e5f-108">Prerequisites</span></span>

* <span data-ttu-id="c1e5f-109">Hdınsight kümesi Hadoop'ta.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="c1e5f-110">Linux tabanlı veya Windows tabanlı kümeler çalışır.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c1e5f-111">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c1e5f-112">Daha fazla bilgi için bkz: [Hdınsight 3.3 devre dışı bırakma](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c1e5f-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c1e5f-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="c1e5f-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="c1e5f-114">SQuirreL JDBC istemci uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="c1e5f-115">Merhaba [Java Geliştirme Seti (JDK) sürüm 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="c1e5f-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="c1e5f-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="c1e5f-117">Maven bir projeyi derleme bu makaleyle ilişkili hello projesi tarafından kullanılan sistem Java projeleri için ' dir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="c1e5f-118">JDBC bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="c1e5f-118">JDBC connection string</span></span>

<span data-ttu-id="c1e5f-119">JDBC bağlantıları tooan Hdınsight kümesine Azure üzerinde 443 yapılır ve hello trafiği güvenliğinin SSL ile.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="c1e5f-120">arkasında hello kümeleri sit hello arası ortak ağ geçidi HiveServer2 gerçekten dinlediği hello trafiği toohello bağlantı noktası yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="c1e5f-121">Merhaba, bir örnek bağlantı dizesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="c1e5f-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="c1e5f-122">Değiştir `CLUSTERNAME` Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="c1e5f-123">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c1e5f-123">Authentication</span></span>

<span data-ttu-id="c1e5f-124">Merhaba bağlantı kurulurken hello Hdınsight Küme Yönetici adı ve parola tooauthenticate toohello küme ağ geçidi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="c1e5f-125">SQuirreL SQL gibi JDBC istemcilerinden bağlanırken istemci ayarları'nda hello yönetici adı ve parola girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="c1e5f-126">Bir Java uygulamasında bir bağlantı kurulurken hello adını ve parolasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="c1e5f-127">Örneğin, hello aşağıdaki Java kod hello bağlantı dizesi, yönetici adı ve parola kullanarak yeni bir bağlantı açar:</span><span class="sxs-lookup"><span data-stu-id="c1e5f-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="c1e5f-128">SQuirreL SQL istemci ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="c1e5f-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="c1e5f-129">SQuirreL SQL çalıştırmak kullanılan tooremotely Hive sorguları Hdınsight kümenize ile olabilecek bir JDBC istemcidir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="c1e5f-130">Merhaba aşağıdaki adımlarda SQuirreL SQL zaten yüklemiş olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="c1e5f-131">Merhaba Hive JDBC sürücülerini Hdınsight kümenize kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="c1e5f-132">İçin **Linux tabanlı Hdınsight**, kullanım hello aşağıdaki adımları toodownload gerekli hello jar dosyalarını.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="c1e5f-133">Merhaba dosyaları içeren bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="c1e5f-134">Örneğin, `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="c1e5f-135">Bir komut satırından toocopy hello hello Hdınsight kümesi dosyalarından kullanım hello aşağıdaki komutlar:</span><span class="sxs-lookup"><span data-stu-id="c1e5f-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="c1e5f-136">Değiştir `USERNAME` hello küme için hello SSH kullanıcı hesabı adı ile.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="c1e5f-137">Değiştir `CLUSTERNAME` hello Hdınsight küme adı ile.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="c1e5f-138">İçin **Windows tabanlı Hdınsight**, kullanım hello aşağıdaki adımları toodownload hello jar dosyalarını.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="c1e5f-139">Hello Azure portal, Hdınsight kümenize seçin ve ardından hello seçin **Uzak Masaüstü** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Uzak Masaüstü simgesi](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="c1e5f-141">Merhaba Uzak Masaüstü dikey penceresinde hello kullan **Bağlan** düğmesini tooconnect toohello küme.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="c1e5f-142">Hello Uzak Masaüstü etkin değilse hello form tooprovide bir kullanıcı adı ve parolayı kullanın ve ardından **etkinleştirmek** hello kümesi için Uzak Masaüstü tooenable.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Uzak Masaüstü dikey penceresi](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="c1e5f-144">Seçtikten sonra **Bağlan**, bir .rdp dosyası indirilir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="c1e5f-145">Bu dosya toolaunch hello uzak masaüstü istemcisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="c1e5f-146">İstendiğinde, hello kullanıcı adını ve Uzak Masaüstü erişimi için girdiğiniz parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="c1e5f-147">Bağlantı kurulduktan sonra hello hello Uzak Masaüstü oturumu tooyour yerel makineden aşağıdaki dosyaları kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="c1e5f-148">Adlı yerel bir dizinde put `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="c1e5f-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-JDBC-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="c1e5f-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="c1e5f-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-Common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="c1e5f-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="c1e5f-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="c1e5f-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="c1e5f-152">hello sürüm numaraları Hello yollarını ve dosya adlarını dahil, kümeniz için farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="c1e5f-153">Merhaba dosyaları kopyalanıyor tamamladıktan sonra hello Uzak Masaüstü oturumu bağlantısını kesin.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="c1e5f-154">Merhaba SQuirreL SQL uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="c1e5f-155">Merhaba penceresinde Hello soldan seçin **sürücüleri**.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Merhaba penceresinin sol tarafındaki hello sürücüler sekmesinde](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="c1e5f-157">Merhaba simgeler hello hello üstündeki gelen **sürücüleri** iletişim, select hello  **+**  simgesi toocreate bir sürücü.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Sürücüleri simgeler](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="c1e5f-159">Merhaba sürücü Ekle iletişim kutusunda, aşağıdaki bilgilerle hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c1e5f-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="c1e5f-160">**Ad**: yığını</span><span class="sxs-lookup"><span data-stu-id="c1e5f-160">**Name**: Hive</span></span>
    * <span data-ttu-id="c1e5f-161">**Örnek URL**:`jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="c1e5f-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="c1e5f-162">**Ek sınıf yolu**: indirilen kullanım hello Ekle düğmesi tooadd hello jar dosyaları daha önce</span><span class="sxs-lookup"><span data-stu-id="c1e5f-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="c1e5f-163">**Sınıf adı**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="c1e5f-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![sürücü iletişim ekleyin](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="c1e5f-165">Tıklatın **Tamam** toosave bu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="c1e5f-166">Merhaba SQuirreL SQL penceresinde Hello solda seçin **diğer adlar**.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="c1e5f-167">Merhaba ardından  **+**  simgesi toocreate bir bağlantı diğer adı.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![Yeni diğer ad ekleyin](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="c1e5f-169">Kullanım hello aşağıdaki değerleri Merhaba **diğer ad eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="c1e5f-170">**Ad**: Hdınsight'ta Hive</span><span class="sxs-lookup"><span data-stu-id="c1e5f-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="c1e5f-171">**Sürücü**: kullanım hello açılır tooselect hello **Hive** sürücüsü</span><span class="sxs-lookup"><span data-stu-id="c1e5f-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="c1e5f-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="c1e5f-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="c1e5f-173">Değiştir **CLUSTERNAME** Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="c1e5f-174">**Kullanıcı adı**: Hdınsight kümenizin hello küme oturum açma hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="c1e5f-175">Merhaba varsayılan `admin`.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="c1e5f-176">**Parola**: hello hello küme oturum açma hesabının parolasını.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-176">**Password**: hello password for hello cluster login account.</span></span>

 ![diğer iletişim ekleyin](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="c1e5f-178">Kullanım hello **Test** bağlantı works hello düğmesi tooverify.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="c1e5f-179">Zaman **bağlanın: Hdınsight'ta Hive** seçin iletişim kutusu görüntülenirse, **Bağlan** tooperform hello test.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="c1e5f-180">Gördüğünüz Hello testi başarılı olursa bir **bağlantı başarılı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="c1e5f-181">toosave hello bağlantısı diğer adı hello kullan **Tamam** düğmesi hello hello sonundaki **diğer ad eklemek** iletişim.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="c1e5f-182">Merhaba gelen **bağlanmak** SQuirreL SQL hello üstündeki açılan seçin **Hdınsight'ta Hive**.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="c1e5f-183">İstendiğinde, seçin **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-183">When prompted, select **Connect**.</span></span>

    ![Bağlantı iletişim kutusu](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="c1e5f-185">Bağlantı kurulduktan sonra aşağıdaki sorgu hello SQL sorgusu iletişim kutusuna ve ardından hello seçin hello girin **çalıştırmak** simgesi.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="c1e5f-186">Hello sonuçları alanı hello hello sorgunun sonuçlarını göstermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![Sonuçları dahil olmak üzere sql sorgu iletişim kutusu](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="c1e5f-188">Bir örnek Java uygulaması Bağlan</span><span class="sxs-lookup"><span data-stu-id="c1e5f-188">Connect from an example Java application</span></span>

<span data-ttu-id="c1e5f-189">Java istemci tooquery Hive kullanarak bir örnek kullanılabilir [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="c1e5f-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="c1e5f-190">Merhaba depo toobuild Hello yönergeleri izleyin ve hello örnek çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c1e5f-191">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c1e5f-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="c1e5f-192">Çalışırken tooopen SQL Bağlantısı beklenmeyen bir hata oluştu</span><span class="sxs-lookup"><span data-stu-id="c1e5f-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="c1e5f-193">**Belirtiler**: sürüm 3.3 veya 3.4 tooan Hdınsight kümesi bağlanırken beklenmeyen bir hata oluştu hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="c1e5f-194">Bu hata Hello yığın izlemesi satırlardan hello ile başlar:</span><span class="sxs-lookup"><span data-stu-id="c1e5f-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="c1e5f-195">**Neden**: Bu hata SQuirreL ve hello bir hello Hive JDBC bileşenleri tarafından zorunlu tarafından kullanılan hello commons codec.jar dosyası hello sürümündeki bir uyuşmazlık kaynaklanır.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="c1e5f-196">**Çözümleme**: Bu hata, kullanım hello aşağıdaki adımları toofix:</span><span class="sxs-lookup"><span data-stu-id="c1e5f-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="c1e5f-197">Hdınsight kümenize Hello commons codec jar dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="c1e5f-198">SQuirreL çıkın ve ardından SQuirreL, sisteminizde yüklü olduğu toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="c1e5f-199">Merhaba altındaki hello SquirreL dizininde `lib` dizini Değiştir hello varolan commons-codec.jar bir indirilen hello Hdınsight kümeden hello ile.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="c1e5f-200">SQuirreL yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-200">Restart SQuirreL.</span></span> <span data-ttu-id="c1e5f-201">Merhaba hata artık hdınsight'ta tooHive bağlanırken olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1e5f-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c1e5f-202">Next steps</span></span>

<span data-ttu-id="c1e5f-203">Göre nasıl toouse JDBC toowork Hive, aşağıdaki kullanım hello ile diğer yolları toowork Azure Hdınsight ile tooexplore bağlar öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="c1e5f-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="c1e5f-204">Veri tooHDInsight karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="c1e5f-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="c1e5f-205">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="c1e5f-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c1e5f-206">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="c1e5f-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c1e5f-207">HDInsight ile MapReduce işleri kullanma</span><span class="sxs-lookup"><span data-stu-id="c1e5f-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
