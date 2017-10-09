---
title: "hdınsight'ta - Azure R Server aaaGet Başlarken | Microsoft Docs"
description: "Merhaba kümesinde bir R betiği göndermek ve nasıl toocreate bir Apache Spark R Server içeren Hdınsight kümesinde öğrenin."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>HDInsight üzerinde R Server kullanmaya başlayın

Hdınsight Hdınsight kümenize tümleşik bir R Server seçeneği toobe içerir. Bu seçenek R betiklerini toouse Spark ve MapReduce dağıtılmış toorun hesaplamalar sağlar. Bu belgede nasıl toocreate Hdınsight kümesi ve için Spark kullanarak gösteren Çalıştır bir R betiği bir R Server'a R hesaplamaları dağıtılmış öğrenin.


## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**: Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir. Git toohello makale [alma Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) daha fazla bilgi için.
* **Bir güvenli Kabuk (SSH) istemcisi**: bir SSH istemcisi kullanılır tooremotely toohello Hdınsight kümesine bağlanın ve doğrudan hello kümede komutları çalıştırın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma.](hdinsight-hadoop-linux-use-ssh-unix.md)
* **SSH anahtarları (isteğe bağlı)**: hello SSH kullanılan hesap tooconnect toohello küme bir parola veya ortak anahtar kullanılarak güvenli hale getirebilirsiniz. Bir parola kullanarak kolaydır ve bir genel/özel anahtar çifti toocreate gerek kalmadan, tooget başlatılan sağlar. Ancak, bir anahtar kullanılması daha güvenlidir.

> [!NOTE]
> Bu belgedeki Hello adımlar bir parola kullandığınızı varsayar.


## <a name="automated-cluster-creation"></a>Otomatik küme oluşturma

Azure Resource Manager şablonları, hello SDK ve aynı zamanda PowerShell kullanarak, Hdınsight R sunucularını hello oluşturulmasını otomatik hale getirebilirsiniz.

* bir Azure kaynak yönetimi şablonu kullanarak bir R Server toocreate bkz [R server Hdınsight kümesi dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* R Server hello .NET SDK kullanarak bir toocreate bakın [hello .NET SDK kullanarak Hdınsight'ta Linux tabanlı kümelerde oluşturma.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* R Server toodeploy powershell kullanarak hello makaleye bakın üzerinde [PowerShell ile hdınsight'ta R Server oluşturma](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Hello Azure portal kullanarak hello kümesi oluşturma

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. **YENİ** -> **Zeka + Analiz**, -> **HDInsight** seçeneklerini belirtin.

    ![Yeni küme oluşturma görüntüsü](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. Merhaba, **hızlı Oluştur** deneyimi, hello hello küme adı **küme adı** alan. Birden çok Azure aboneliğiniz varsa, hello kullan **abonelik** toouse istediğiniz girişi tooselect hello biri.

    ![Küme adı ve abonelik seçimleri](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Seçin **küme türü** tooopen hello **küme yapılandırması** dikey. Merhaba üzerinde **küme yapılandırması** dikey penceresinde, aşağıdaki seçenekleri şu select hello:

    * **Küme Türü**: R Server
    * **Sürüm**: R Server tooinstall hello kümede select hello sürümü. şu anda kullanılabilir Hello sürüm ***R Server 9.1 (HDI 3.6)***. Sürüm Notları hello kullanılabilir R Server sürümleri için kullanılabilir [burada](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **R Server için R Studio community edition**: Bu tarayıcı tabanlı IDE hello edge düğüm üzerinde varsayılan olarak yüklenir. Toonot tercih ederseniz yüklemediyseniz, ardından hello onay kutusunun işaretini kaldırın. Toohave seçerseniz yüklü, bir kez oluşturulduğunda Rstudio'dan sunucu oturum açma kümeniz için bir portal uygulaması dikey penceresinde bulunur hello erişmek için hello URL.
    * Bırakın hello diğer seçenekleri hello varsayılan değerlerinde ve hello kullan **seçin** düğme toosave hello küme türü.

        ![Küme türü dikey penceresi ekran görüntüsü](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Bir **Küme oturum açma kullanıcı adı** ve **Küme oturum açma parolası** girin.

    Bir **SSH Kullanıcı Adı** belirtin. SSH kullanılan tooremotely Bağlan toohello küme kullanarak bir **güvenli Kabuk (SSH)** istemci. Merhaba SSH kullanıcı ya da, bu iletişim kutusunda veya (içinde Merhaba yapılandırma sekmesi hello küme için) hello Küme oluşturulduktan sonra da belirtebilirsiniz. R sunucusudur yapılandırılmış tooexpect bir **SSH kullanıcı adı** "remoteuser" olarak.  **Farklı bir kullanıcı adı kullanırsanız, hello Küme oluşturulduktan sonra ek bir adım gerçekleştirmeniz gerekir.**

    İçin işaretli bırakın hello kutusunda **küme oturum açma aynı parolayı kullanın** toouse **parola** hello kimlik doğrulaması türü olarak bir ortak anahtar kullanımını tercih sürece.  Örneğin, RTVS, Rstudio'dan veya başka bir masaüstü IDE olarak uzak istemciye aracılığıyla hello kümede ortak/özel anahtar çifti tooaccess R Server gerekir. Merhaba Rstudio'dan Server community edition yüklerseniz, toochoose bir SSH parolası gerekir.     

    toocreate ve kullanım bir genel/özel anahtar çifti işaretini **küme oturum açma aynı parolayı kullanın** ve ardından **ortak anahtar** ve aşağıdaki gibi ilerleyin. Bu yönergelerde, ssh-keygen veya eşdeğeri ile birlikte Cygwin'in yüklü olduğu varsayılır.

    * Dizüstü bilgisayarınızda hello komut isteminden bir genel/özel anahtar çifti oluşturur:

        ssh-keygen -t rsa -b 2048

    * Merhaba komut istemi tooname bir anahtar dosyası izleyin ve sonra ek güvenlik için bir parola girin. Ekranınızın hello görüntü aşağıdaki gibi görünmelidir:

        ![Windows'da SSH cmd satırı](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Bu komut, özel bir anahtar dosyası ve hello ad < özel anahtarı dosyaadı > .pub, örneğin furiosa ve furiosa.pub altında ortak bir anahtar dosyası oluşturur.

        ![SSH dir](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Merhaba ortak anahtar dosyası (&#42;. belirtin HDI atama ve kimlik bilgilerinin küme kaynak grubu ve bölge ve select onaylamadan pub) **sonraki**.

        ![Kimlik Bilgileri dikey penceresi](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Dizüstü bilgisayarınızda hello özel keyfile üzerindeki izinleri değiştirin:

        chmod 600 <private-key-filename>

   * Merhaba özel anahtar dosyası SSH ile uzaktan oturum açma için kullanın:

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      Ya da bölümü hello tanımı, Hadoop Spark olarak bağlamı için R Server hello istemcide işlem. Merhaba bkz **kullanarak Microsoft R Server Hadoop istemcisi olarak** içinde alt bölüm [bir işlem bağlamı için Spark oluşturma](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Merhaba hızlı Oluştur toohello geçişleri **depolama** hello birincil konumunu hello için kullanılan ayarları toobe HDFS dosya sistemi hello küme tarafından kullanılan dikey tooselect hello depolama hesabı. Yeni veya mevcut bir Azure Depolama hesabını ya da mevcut bir Data Lake Storage hesabını seçin.

    - Bir Azure depolama hesabı seçin, mevcut bir depolama hesabını seçerek seçilirse **bir depolama hesabı seçin** ve hello ilgili hesabı seçme. Hello kullanarak yeni bir hesap oluşturma **Yeni Oluştur** hello bağlantıyı **bir depolama hesabı seçin** bölümü.

      > [!NOTE]
      > Seçerseniz **yeni** hello yeni depolama hesabı için bir ad girmeniz gerekir. Merhaba adı kabul edilirse yeşil bir onay işareti görünür.

      Merhaba **varsayılan kapsayıcı** Varsayılanları toohello hello kümenin adını. Bu varsayılan hello değeri bırakın.

      Yeni bir depolama hesabı seçeneği seçildiyse, bir komut istemi tooselect **konumu** olan tooselect hangi bölge toocreate hello depolama hesabı.  

         ![Veri kaynağı dikey penceresi](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Merhaba varsayılan veri kaynağı için başlangıç konumu seçerek hello Hdınsight kümesi hello konumunu ayarlar. Merhaba küme ve varsayılan veri kaynağı hello olmalıdır aynı bölgede.

    - Toouse mevcut bir Data Lake Store istiyorsanız, seçip hello ADLS depolama hesabı toouse ve hello küme eklemek *Ekle* kimlik tooyour küme tooallow erişim toohello deposu. Bu işlem hakkında daha fazla bilgi için [Azure portalı kullanarak Data Lake Store ile HDInsight kümesi oluşturma](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal) bölümünü inceleyin.

    Kullanım hello **seçin** düğmesini toosave hello veri kaynağı yapılandırması.


7. Merhaba **Özet** dikey penceresinde tüm ayarlarınızı sonra toovalidate görüntüler. Burada değiştirebilirsiniz, **küme boyutu** toomodify hello Kümenizdeki sunucuların sayısını ve ayrıca herhangi belirtmek **betik eylemleri** toorun istiyor. Daha büyük bir küme gerekir bilmiyorsanız, çalışan düğüm sayısı hello hello varsayılan olarak bırakın `4`. Merhaba hello küme maliyetini hello Dikey içinde gösterilen tahmin.

    ![küme özeti](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Gerekirse, kümenizi hello Portal aracılığıyla daha sonra yeniden boyutlandırabilirsiniz (**küme** -> **ayarları** -> **ölçekte küme**) tooincrease veya Merhaba çalışan düğümü sayısını azaltın.  Bu yeniden boyutlandırma hello küme kullanılmadığında aşağı idling için ya da kapasite toomeet hello büyük görevleri ihtiyaçlarını eklemek için yararlı olabilir.
   >
   >

   Küme, hello veri düğümlerini ve hello kenar düğümüne boyutlandırma zaman aklınızda bazı etkenler tookeep şunları içerir:  

   * Merhaba veriler büyük olduğunda Spark üzerinde dağıtılmış R Server çözümlemeler hello performansını orantılı toohello çalışan düğümlerinin sayısıdır.  

   * R Server çözümlemeler Hello performansını çözümlenmekte veri hello boyutunda doğrusal ' dir. Örneğin:  

     * Küçük toomodest verileri için performans yerel işlem bağlamda hello kenar düğümü üzerindeki analiz olduğunda en iyisidir.  Bağlamları hello yerel ve Spark altında işlem hello senaryoları hakkında daha fazla bilgi için en iyi şekilde çalışır, Hdınsight'ta R Server için işlem bağlamı seçenekleri konusuna bakın.<br>
     * Toohello kenar düğümünde oturum açın ve R betiği çalıştırın, ardından hello ScaleR rx-işlevleri dışındaki tüm yürütülen varsa <strong>yerel olarak</strong> hello edge düğüm üzerinde. Bu nedenle bellek hello ve hello kenar düğümüne çekirdek sayısı buna göre boyutlandırılmalıdır. Merhaba R Server HDI üzerinde uzak işlem bağlamı olarak dizüstü bilgisayarınızdan kullanıyorsanız aynı durum geçerlidir.

     ![Düğüm fiyatlandırma katmanları dikey penceresi](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Kullanım hello **seçin** yapılandırma fiyatlandırma düğmesi toosave hello düğümü.

   **Şablon ve parametreleri indirme** bağlantısı da yer almaktadır. Bir küme hello seçili yapılandırma ile kullanılan tooautomate hello oluşturma olabilir Bu bağlantı toodisplay betikleri tıklayın. Oluşturulduktan sonra bu komut dosyalarını da hello kümeniz için Azure portal giriş mevcuttur.

   > [!NOTE]
   > Oluşturulan, genellikle yaklaşık 20 dakika hello küme toobe için biraz zaman alabilir. Merhaba döşeme Sabitle hello üzerinde kullanın ya da hello **bildirimleri** hello girişinde sol hello sayfa toocheck hello oluşturma işlemi.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>TooRStudio sunucusuna bağlan

Daha sonra tooinclude Rstudio'dan Server community edition yüklemenizde seçtiyseniz hello Rstudio'dan oturum açma iki farklı yöntem aracılığıyla erişebilirsiniz.

1. URL aşağıdaki toohello gidin (burada **CLUSTERNAME** oluşturduğunuz hello küme hello adıdır):

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. Kümeniz için hello girişi hello Azure portal, select hello açmak **R Server panolar** hızlı bağlantıyı ve hello seçme **R Studio Pano**:

     ![Erişim hello R studio Panosu](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Erişim hello R studio Panosu](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Kullanılan hello yönteminden bağımsız olarak hello ilk kez oturum açtığınızda, tooauthenticate iki kez gerekir.  Merhaba ilk kimlik doğrulaması sırasında hello sağlamak *yönetici UserID küme* ve *parola*. Merhaba ikinci isteminde hello sağlamak *SSH UserID* ve *parola*. Sonraki günlüğü bileşenler yalnızca hello gerektiren *SSH parolası* ve *UserID*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Toohello R Server edge düğümüne bağlanma

TooR Server edge düğümüne hello Hdınsight kümesinin hello komutuyla SSH kullanarak bağlanın:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Merhaba bulabilirsiniz `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` hello sonra kümenizi seçerek Azure portal adresi **tüm ayarları** -> **uygulamaları** -> **RServer**. Merhaba hello kenar düğümüne SSH uç nokta bilgileri görüntüler.
>
> ![Merhaba SSH uç noktası hello kenar düğümüne görüntüsü](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

SSH kullanıcı hesabınızın parolası toosecure kullandıysanız, istendiğinde tooenter olan bu. Bir ortak anahtar kullandıysanız, toouse hello olabilir `-i` parametresi toospecify hello eşleşen özel anahtarı. Örneğin:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Daha fazla bilgi için bkz: [tooHDInsight (Hadoop) SSH kullanarak bağlanmak](hdinsight-hadoop-linux-use-ssh-unix.md).

Bağlantı kurulduktan sonra bir komut istemi benzer toohello şu ulaşır:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Birden çok eş zamanlı kullanıcı etkinleştirme

Daha fazla kullanıcıları için hangi hello Rstudio'dan topluluk sürümünü çalıştıran hello kenar düğümüne ekleyerek, birden çok eşzamanlı kullanıcı etkinleştirebilirsiniz.

Bir HDInsight kümesi oluşturduğunuzda bir HTTP kullanıcısı ve bir SSH kullanıcısı olmak üzere iki kullanıcı sağlamanız gerekir:

![Eşzamanlı kullanıcı 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Oturum açma kullanıcı küme**: kullanılan tooprotect hello Hdınsight olan hello Hdınsight ağ geçidi üzerinden kimlik doğrulaması için bir HTTP kullanıcı oluşturduğunuz kümeleri. Bu HTTP kullanılan tooaccess hello Ambari UI, YARN kullanıcı Arabiriminde yanı sıra, diğer kullanıcı Arabirimi bileşenlerini kullanıcıdır.
- **Güvenli Kabuk (SSH) kullanıcıadı**: Güvenli Kabuk aracılığıyla bir SSH kullanıcı tooaccess hello kümesi. Bu kullanıcı hello Linux sistemi tüm hello baş düğümler, çalışan düğümlerine ve kenar düğümler için de bir kullanıcıdır. Bu nedenle, güvenli Kabuk tooaccess hello düğümün herhangi birinden uzak bir kümede kullanabilirsiniz.

Merhaba Microsoft R Server Hdınsight türü kümede kullanılan hello R Studio Server Community sürümü yalnızca Linux kullanıcı adı ve parola oturum açma mekanizması olarak kabul eder. Belirteç iletmeyi desteklemez. Yeni bir küme oluşturduktan ve toouse R Studio tooaccess istiyorsanız bunu, toolog içinde iki kez gerekir.

- İlk hello Hdınsight ağ geçidi üzerinden hello HTTP kullanıcı kimlik bilgilerini kullanarak oturum açın: 

    ![Eşzamanlı kullanıcı 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Ardından hello SSH kullanıcı kimlik bilgilerini toolog içinde tooRStudio kullanın:
  
    ![Eşzamanlı kullanıcı 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Şu anda bir HDInsight kümesi sağlanırken yalnızca bir SSH kullanıcı hesabı oluşturulabilir. Birden çok kullanıcı tooaccess Microsoft hdınsight'ta R Server tooenable kümeleri şekilde hello Linux sistem toocreate ek kullanıcılar ihtiyacımız var.

Rstudio'dan Server Topluluğu hello kümenin kenar düğümüne üzerinde çalıştığı için burada birkaç adım vardır:

1. Oluşturulan hello SSH kullanıcı toolog toohello kenar düğümünü kullanın
2. Kenar düğümüne daha fazla Linux kullanıcısı ekleme
3. Oluşturulan hello kullanıcıyla Rstudio'dan topluluk sürümünü kullanın

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>1. adım: hello oluşturulan SSH kullanıcı toolog toohello kenar düğümünü kullanın.

Herhangi bir SSH Aracı (örneğin, Putty) indirin ve hello varolan SSH kullanıcı toolog içinde kullanın. Sağlanan hello yönergeleri izleyin [tooHDInsight (Hadoop) SSH kullanarak bağlanmak](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess hello kenar düğümüne. Itanium tabanlı sistemler için Hello edge düğüm adresi R Server için Hdınsight kümesinde: *clustername ed ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>2. Adım: Kenar düğümüne daha fazla Linux kullanıcısı ekleme

bir kullanıcı toohello kenar düğümüne tooadd hello komutları yürütün:

    sudo useradd yournewusername -m
    sudo passwd yourusername

Döndürülen öğe aşağıdaki hello görmeniz gerekir: 

![Eşzamanlı kullanıcı 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

İstendiğinde "geçerli Kerberos Parola:", yalnızca basın **Enter** tooignore onu. Merhaba `-m` seçeneğini `useradd` komutu gösterir hello sistem Rstudio'dan topluluğu sürümü için gerekli olan hello kullanıcı için giriş klasörü oluşturur.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>3. adım: Oluşturulan hello kullanıcıyla kullanım Rstudio'dan topluluğu sürümü

Merhaba kullanıcı tarafından oluşturulmuş toolog içinde tooRStudio kullanın:

![Eşzamanlı kullanıcı 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Bildirim Rstudio'dan hello yeni kullanıcı kullandığınızı gösterir (burada, örneğin, *sshuser6*) hello kümedeki toolog: 

![Eşzamanlı kullanıcı 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

Merhaba özgün kimlik bilgilerini kullanarak da oturum açabilir (varsayılan olarak, olmasından *sshuser*) aynı anda başka bir tarayıcı penceresi öğesinden.

scaleR işlevlerini kullanarak bir iş gönderebilirsiniz. Bir işi hello kullanılan komutlar toorun örneği şöyledir:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Gönderilen Merhaba işleri YARN kullanıcı arabiriminde farklı kullanıcı adları altında olduğuna dikkat edin:

![Eşzamanlı kullanıcı 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Ayrıca bu hello yeni kullanıcılar Linux sistemde kök ayrıcalıkları olmayan, ancak bunlar sahip hello aynı eklenen not tooall hello hello uzak HDFS ve WASB depolama dosyalarında erişin.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Merhaba R Konsolu'nu kullanma

1. Merhaba SSH oturumundan komut toostart hello R konsolundan aşağıdaki hello kullan:  

        R

2. Çıktı benzer toohello aşağıdaki görmeniz gerekir:
    
    R sürüm 3.2.2 (2015-08-14)--"Yangın güvenliği" Telif Hakkı (C) 2015 hello R Foundation istatistiksel bilgi işlem platformu: pc x86_64 için linux gnu (64 bit)

    R ücretsiz bir yazılımdır ve HİÇBİR GARANTİ verilmemektedir.
    Hoş Geldiniz tooredistribute olduğunuz belirli koşullar altında.
    Dağıtım ayrıntıları için "license()" veya "licence()" yazın.

    Doğal dil desteği yalnızca İngilizce için mevcuttur

    R birçok katılımcının rol aldığı ortak bir projedir.
    'Contributors()' toocite R veya R yayınlarda nasıl paketler daha fazla bilgi ve 'citation()' yazın.

    Bazı gösterileri, çevrimiçi Yardım ' help()' veya 'help.start()' için bir HTML tarayıcı arabirimi toohelp 'demo()' türü.
    'Q()' tooquit r yazın

    Microsoft R Server sürüm 8.0: R Microsoft paketlerinin gelişmiş dağıtımı Telif Hakkı (C) 2016 Microsoft Corporation

    Sürüm notları için "readme()" yazın.
    >

3. Merhaba gelen `>` komut istemi, R kodu girin. R server içerir tooeasily izin paketleri Hadoop ile etkileşim kurmanızı ve dağıtılmış hesaplamalar çalıştırın. Örneğin, komut tooview hello kök hello varsayılan dosya sistemi hello Hdınsight kümesi için aşağıdaki hello kullan:

    rxHadoopListFiles("/")

4. Merhaba WASB stili adresleme de kullanabilirsiniz.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Microsoft R Server veya Microsoft R Client uzak örneğinden HDI üzerinde R Server kullanma

Erişim toohello HDI Hadoop Spark işlem bağlamı Microsoft R Server ya da Microsoft R Masaüstü veya dizüstü bilgisayar üzerinde çalışan istemci uzak bir örnekten olası tooset olur. Bkz: **kullanarak Microsoft R Server Hadoop istemcisi olarak** alt bölümde hello [bir işlem bağlamı için Spark oluşturma](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo toospecify hello hello RxSpark işlem bağlamı dizüstü bilgisayarınızda tanımlarken, aşağıdaki seçenekleri şu nedenle ihtiyacınız: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches ve sshProfileScript. Örneğin:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>İşlem bağlamı kullanma

Hesaplama yerel olarak hello edge düğüm üzerinde gerçekleştirilen ya da hello Hdınsight kümesi hello düğümler dağıtılmış bir işlem bağlamında toocontrol sağlar.

1. Rstudio'dan sunucu veya hello R konsolunda (bir SSH oturumu), kod tooload örnek verileri hello varsayılan depolama alanına Hdınsight için aşağıdaki hello kullan:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Ardından, şimdi bazı veri bilgileri oluşturun ve biz hello verilerle çalışmak için iki veri kaynaklarını tanımlayın.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Şimdi Lojistik regresyon hello yerel işlem bağlamı kullanarak hello verileri çalıştırın.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Satırları benzer toohello aşağıdaki ile biten bir çıktı görmeniz gerekir:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Ardından, Şimdi Çalıştır hello hello Spark bağlamını kullanarak aynı Lojistik regresyon. Merhaba Spark bağlam hello Hdınsight kümesindeki tüm hello alt düğümler üzerinden işleme hello dağıtır.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > Küme düğümleri arasında MapReduce toodistribute hesaplama de kullanabilirsiniz. İşlem bağlamı hakkında daha fazla bilgi için bkz. [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](hdinsight-hadoop-r-server-compute-contexts.md).


## <a name="distribute-r-code-toomultiple-nodes"></a>R kodu toomultiple düğümleri Dağıt

R Server ile kolayca var olan R kodu alın ve çalıştırın hello kümedeki birden çok düğüm arasında kullanarak `rxExec`. Bu işlev bir parametre tarama veya benzetme işlemi sırasında yararlıdır. Merhaba aşağıdaki kodu nasıl örneğidir toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Merhaba Spark veya MapReduce bağlamı hala kullanıyorsanız, bu komut hello nodename değeri hello çalışan düğümleri için bu hello kodu döndürür. `(Sys.info()["nodename"])` çalıştırıldığı. Örneğin, dört düğümlü bir küme üzerinde tooreceive benzer toohello şu çıktıları bekler:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Hive ve Parquet Verilerine Erişim

R Server 9.1 içinde kullanılabilecek bir özellik hello Spark işlem bağlamında ScaleR işlevleri tarafından kullanım için doğrudan erişim toodata Hive ve Parquet sağlar. Bu özellikler, Spark SQL tooload verileri kullanarak Spark DataFrame ScaleR göre Analiz için doğrudan çalışan RxHiveData ve RxParquetData adlı yeni ScaleR veri kaynağı işlevler aracılığıyla kullanılabilir.  

koddan hello bazı örnek kod kullanımda hello yeni işlevleri sağlar:

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Bu yeni işlevler kullanımı ile ilgili ek bilgi için hello hello aracılığıyla R Server'ın çevrimiçi yardımına bakın `?RxHivedata` ve `?RxParquetData` komutları.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Ek R paketleri hello kenar düğümüne yükleyin

Merhaba kenar düğümüne tooinstall ek R paketlerini istiyorsanız kullanabileceğiniz `install.packages()` doğrudan bağlı toohello kenar zaman SSH düğümünden içinden R konsol hello. Ancak, tooinstall R paketleri hello kümenin hello alt düğümlerinde gerekiyorsa, bir komut dosyası eylemi kullanmanız gerekir.

Betik eylemleri kullanılan toomake yapılandırma değişiklikleri toohello Hdınsight küme veya tooinstall ek yazılım, ek R paketleri gibi olan Bash betikleridir. Betik eylemi kullanarak ek paketleri tooinstall hello aşağıdaki adımları kullanın:

> [!IMPORTANT]
> Merhaba Küme oluşturulduktan sonra betik eylemleri tooinstall ek R paketlerini kullanma yalnızca kullanılabilir. Merhaba betik R Server tamamen yüklenmiş ve yapılandırılmış dayanır olarak küme oluşturma sırasında bu yordamı kullanmayın.
>
>

1. Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümesinde R sunucunuzu seçin.

2. Merhaba gelen **ayarları** dikey penceresinde, select **betik eylemleri** ve ardından **gönderme yeni** toosubmit yeni betik eylemi.

   ![Betik eylemleri dikey penceresinin görüntüsü](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. Merhaba gelen **betik eylemi Gönder** dikey penceresinde, aşağıdaki bilgilerle hello sağlayın:

   * **Ad**: kolay bir tooidentify bu komut dosyası adı

   * **Bash betiği URI’si**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Başlık**: Bu öğenin **işareti kaldırılmış** olmalıdır

   * **Çalışan**: Bu öğe **işaretlenmiş** olmalıdır

   * **Kenar düğümleri**: Bu öğenin **işareti kaldırılmış** olmalıdır.

   * **Zookeeper**: Bu öğenin **işareti kaldırılmış** olmalıdır

   * **Parametreleri**: hello R paketleri yüklü toobe. Örneğin, `bitops stringr arules`

   * **Bu betiği kalıcı yap...** : Bu öğe **İşaretlenmiş** olmalıdır  

   > [!NOTE]
   > 1. Varsayılan olarak, tüm R paketleri hello Microsoft MRAN depo hello yüklü R Server sürümüyle tutarlı bir anlık yüklenir. Paketler daha yeni sürümleri tooinstall istiyorsanız, bazı riskini uyumsuzluk yoktur. Ancak bu tür bir yükleme belirterek mümkündür `useCRAN` hello ilk hello paketinin liste öğesi, örneğin `useCRAN bitops, stringr, arules`.  
   > 2. Bazı R paketleri için ek Linux sistem kitaplıkları gerekir. Kolaylık olması için biz hello ilk 100 en popüler R paketi tarafından gerekli hello bağımlılıkları önceden yüklediniz. Ancak, bunlar dışında kitaplıkları hello R paketleri yüklemeniz gerekiyorsa ardından burada kullanılan hello temel komut dosyasını karşıdan yükleyin ve adımları tooinstall hello sistem kitaplıkları eklemeniz gerekir. Karşıya yükleme değiştiren hello betik tooa genel Azure depolama kapsayıcıda blob ve değiştiren hello betik tooinstall hello paketlerini kullanma sonra yapmanız gerekir.
   >    Betik Eylemleri geliştirme hakkında bilgi için bkz. [Betik Eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Betik eylemi ekleme](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Seçin **oluşturma** toorun hello komut dosyası. Merhaba betik tamamlandıktan sonra tüm çalışan düğümleri üzerinde hello R paketleri kullanılabilir.


## <a name="using-microsoft-r-server-operationalization"></a>Microsoft R Server ile Kullanıma Hazır Hale Getirme

Veri modellemesi tamamlandığında hello modeli toomake tahminleri faaliyete geçirebilirsiniz. Microsoft R Server operationalization tooconfigure hello aşağıdaki adımları gerçekleştirin:

İlk olarak, ssh hello kenar düğümüne içine. Örneğin, 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

SSH kullandıktan sonra hello ilgili sürümü ve sudo hello dotnet dll dizini değiştirin: 

- Microsoft R Server 9.1 için:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Microsoft R Server 9.0 için:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

Bir çalıştırma yapılandırmasıyla tooconfigure Microsoft R Server operationalization hello aşağıdaki:

1. "R Server'ı Kullanıma Hazır Hale Getirmek için Yapılandır" seçeneğini belirleyin
2. “A. One-box (web + işlem düğümleri)” öğesini seçin
3. Hello için bir parola girmenizi **yönetici** kullanıcı

![one box işlemi](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

İsteğe bağlı bir adım olarak aşağıdaki şekilde bir tanılama testi çalıştırarak Tanılama denetimleri gerçekleştirebilirsiniz:

1. “6. Tanılama testleri çalıştır” öğesini seçin
2. “A. Test yapılandırması” öğesini seçin
3. Kullanıcı adı olarak "admin" değerini ve önceki yapılandırma adımında belirtilen parolayı girin
4. Genel Sistem Durumunu Onayla = başarılı
5. Çıkış hello yönetim yardımcı programı
6. SSH’den çıkın

![İşlem için tanılama](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Spark’ta web hizmeti tüketilirken uzun gecikmeler**
>
>Tooconsume bir web hizmeti çalışıyor Spark işlem bağlamda mrsdeploy işlevlerle oluşturduğunuzda gecikmelere karşılaşırsanız, bazı eksik klasörler tooadd gerekebilir. Merhaba Spark uygulama ait tooa kullanıcı olarak adlandırılır ve '*rserve2*' ne zaman onu çağrılır mrsdeploy işlevleri kullanarak bir web hizmetinden. Bu soruna geçici bir çözüm toowork:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


Bu aşamada Operationalization hello yapılandırması tamamlanır. Kullanabileceğiniz artık hello 'mrsdeploy' paketini kenar düğümünü, RClient tooconnect toohello Operationalization üzerinde ve özellikleri gibi kullanmaya başlamak [uzaktan yürütme](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) ve [web Hizmetleri](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). Olup, küme üzerinde bir sanal ağ veya kurulduğuna bağlı olarak, yukarı bağlantı noktası aracılığıyla SSH oturum iletme tünel tooset gerekebilir. Merhaba aşağıdaki bölümlerde açıklanmıştır nasıl tooset bu tünel ayarlama.

### <a name="rserver-cluster-on-virtual-network"></a>Sanal ağda RServer Kümesi

Bağlantı noktası 12800 toohello kenar düğümüne üzerinden trafiğe izin emin olun. Bu şekilde hello kenar düğümü tooconnect toohello Operationalization özelliğini kullanabilirsiniz.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Merhaba, `remoteLogin()` olamaz toohello kenar düğümüne bağlanmak ancak SSH toohello kenar düğümünü kullanabilirsiniz, ardından bağlantı noktası 12800 hello kural tooallow trafiğine düzgün ya da olmasın ayarlanmış olup olmadığını tooverify gerekir. Tooface hello sorunu devam ederseniz, bu bağlantı noktası iletme SSH tünel yukarı ayarlayarak çalışabilir. Merhaba bölümü aşağıdaki yönergeler için bkz.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>Sanal ağda RServer Kümesi ayarlanmamış

Kümeniz sanal üzerinde ayarlanmamışsa veya sanal ağ üzerinden bağlantı kurma sorunları yaşıyorsanız, SSH bağlantı noktası iletme tünelini kullanabilirsiniz:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Putty üzerinde de bu ayarı yapabilirsiniz.

![putty ssh bağlantısı](./media/hdinsight-hadoop-r-server-get-started/putty.png)

SSH oturumunuzun etkinleştirildikten sonra makinenizin bağlantı noktası 12800 hello trafiğinden toohello kenar düğümün bağlantı noktası 12800 SSH oturumu üzerinden iletilir. `remoteLogin()` yönteminizde `127.0.0.1:12800` kullandığınızdan emin olun. Bu bağlantı noktası iletme aracılığıyla toohello kenar düğümün operationalization kaydeder.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Nasıl tooscale Microsoft R Server Operationalization işlem düğümleri Hdınsight çalışan düğümleri üzerinde

### <a name="decommission-hello-worker-nodes"></a>Merhaba çalışan düğümü yetkisini alma

Microsoft R Server şu anda Yarn üzerinden yönetilmemektedir. Merhaba çalışan düğümleri yetkisi alınmış emin değilseniz, hello Yarn Kaynak Yöneticisi'ni hello sunucu tarafından gerçekleştirilecek hello kaynakları farkında olmayacağı için beklendiği gibi çalışmaz. Sipariş tooavoid bu durum hello işlem düğümleri ölçeklendirme önce hello çalışan düğümleri yetkisini öneririz.

Adımları toodecommissioning alt düğümleri:

* TooHDI kümenin Ambari konsolunda oturum açın ve "ana" sekmesini tıklatın
* Çalışan düğümü (kullanımdan toobe) seçin, "Eylemler" > "Seçilen konaklar" > "Ana" > "Kapatma üzerinde Bakım modu üzerinde"'i tıklatın. Örneğin, görüntü aşağıdaki hello biz wn3 ve wn4 toodecommission seçtiniz.  

   ![çalışan düğümlerinin yetkisini alma](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* **Eylemler** > **Seçili Ana Bilgisayarlar** > **DataNodes** > öğesini seçip **Yetkisini Al** öğesine tıklayın
* **Eylemler** > **Seçili Ana Bilgisayarlar** > **NodeManagers** > öğesini seçip **Yetkisini Al** öğesine tıklayın
* **Eylemler** > **Seçili Ana Bilgisayarlar** > **DataNodes** > öğesini seçip **Durdur** öğesine tıklayın
* **Eylemler** > **Seçili Ana Bilgisayarlar** > **NodeManagers** > öğesini seçip **Durdur** öğesine tıklayın
* **Eylemler** > **Seçili Ana Bilgisayarlar** > **Ana Bilgisayarlar** > öğesini seçip **Tüm Bileşenleri Durdur** öğesine tıklayın
* Merhaba çalışan düğümleri seçimini kaldırın ve hello baş düğümler seçin
* **Eylemler** > **Seçili Ana Bilgisayarlar** > **Ana Bilgisayarlar** > **Tüm Bileşenleri Yeniden Başlat** öğesini seçin

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Yetkisi alınan her çalışan düğümü üzerinde İşlem düğümlerini yapılandırın

1. Yetkisi alınan her çalışan düğümüne SSH uygulayın.
2. `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll` kullanarak yönetici yardımcı programını çalıştırın.
3. "1" tooselect seçeneği "R Server Operationalization için yapılandırma" girin.
4. "C"c"tooselect seçeneği girin İşlem düğümü" öğesini seçin. Bu, hello çalışan düğümünde hello işlem düğümü yapılandırır.
5. Çıkış hello yönetim yardımcı programı.

### <a name="add-compute-nodes-details-on-web-node"></a>Web Düğümüne işlem düğümleri ekleme

Tüm yetkisi alınmış çalışan düğümleri yapılandırdıktan sonra toorun işlem düğümü, hello kenar düğümüne geri dönün ve hello Microsoft R Server web düğümün yapılandırmasında yetkisi alınmış çalışan düğümleri IP adreslerini ekleyin:

* Merhaba kenar düğümüne içine SSH.
* `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json` öğesini çalıştırın.
* Merhaba "URI'ler" bölümüne bakın ve alt düğümün IP ve bağlantı noktası ayrıntıları ekleyin.

    ![çalışan düğümlerinin yetkisini alma komut satırı](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Sonraki adımlar

Şimdi nasıl toocreate kullanarak hello R Server ve hello temellerini içeren yeni bir Hdınsight kümesi hello bir SSH oturumu R konsolundan anlamanız gerekir. Merhaba aşağıdaki konularda yönetme ve hdınsight'ta R Server ile çalışma diğer yolları açıklanır:

* [(Küme oluşturma sırasında yüklü değilse) Rstudio'dan sunucu tooHDInsight Ekle](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight üzerinde R Server için Azure Depolama seçenekleri](hdinsight-hadoop-r-server-storage.md)
