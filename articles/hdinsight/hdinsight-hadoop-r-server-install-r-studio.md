---
title: "R Server hdınsight'ta - Azure ile Rstudio'dan aaaInstall | Microsoft Docs"
description: "Nasıl tooinstall Rstudio'dan hdınsight'ta R Server ile."
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 918abb0d-8248-4bc5-98dc-089c0e007d49
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3a23021fcf99217e8f551f8b2e89bf1f1e5b967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-rstudio-with-r-server-on-hdinsight"></a>Hdınsight'ta R Server ile Rstudio'dan yükleme

Nasıl tooinstall hello community (ücretsiz) sürümünü bu makalede [Rstudio'dan Server](https://www.rstudio.com/products/rstudio-server/) özel bir komut dosyası kullanarak bir kümesinin hello kenar düğümüne. Rstudio'dan sunucusu, uzak istemciler tarafından kullanılacak tarayıcı tabanlı bir IDE sağlar ve Linux üzerinde yaygın olarak kullanılır. Dahil olmak üzere birden çok tümleşik geliştirme ortamı (IDE) R için kullanılabilir bugün vardır:

- Microsoft'un [R araçları Visual Studio için](https://www.visualstudio.com/en-us/features/rtvs-vs.aspx) (RTVS) 
- [Rstudio'dan sunucu](https://www.rstudio.com/products/rstudio-server/) 
- Walware Eclipse tabanlı [StatET](http://www.walware.de/goto/statet).

Merhaba kenar düğümüne Hdınsight kümesi Rstudio'dan sunucusu yükleme hello avantajı, tam IDE deneyimi hello geliştirme ve R betiklerinin yürütülmesi için R Server ile Merhaba kümede sağlamasıdır. Bu yapılandırma önemli ölçüde daha üretken hello R konsol varsayılan kullanımını olabilir.

> [!NOTE]
> Bu makalede açıklanan hello yordamı yalnızca kümeniz sağlamada tooinstall Rstudio'dan Server community edition seçmediğiniz geçerlidir. Sağlama işlemi sırasında eklediyseniz sonra onu tıklattığınız hello üzerinde tooaccess **R Server panolar** hello Azure portal giriş kümenizin sonra hello parçasında **R Studio Server** döşeme. 

Toouse ticari lisanslı hello Pro Rstudio'dan Server sürümünü tercih ederseniz, hello yükleme yönergeleri izlemeniz gereken [Rstudio'dan Server](https://www.rstudio.com/products/rstudio/download-server/).

> [!NOTE]
> İçin R yüklenen hello kullanarak bir Hdınsight kümesi kullanıyorsanız [yükleme R betik eylemi](hdinsight-hadoop-r-scripts-linux.md), hello adımları bu belgede çalışmaz doğru hello Hdınsight kümesinde bir R Server gerektirir.
>
> 

## <a name="prerequisites"></a>Ön koşullar

* Azure Hdınsight kümesi R Server yüklü. Yönergeler için bkz: [Hdınsight kümelerinde R Server ile çalışmaya başlama](hdinsight-hadoop-r-server-get-started.md).
* Bir SSH istemcisi. Linux ve UNIX dağıtımlarının ya da Macintosh OS X için hello `ssh` komutu hello işletim sistemiyle sağlanan. Windows için öneririz [Cygwin](http://www.redhat.com/services/custom/cygwin/) hello ile [OpenSSH seçeneği](https://www.youtube.com/watch?v=CwYSvvGaiWU), veya [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).  

## <a name="install-rstudio-on-hello-cluster-using-a-custom-script"></a>Özel bir komut dosyası kullanarak hello kümede Rstudio'dan yüklemek

Merhaba adımlar şunlardır:

1. Merhaba kenar düğümüne hello kümesinin tanımlayın. R Server ile bir Hdınsight kümesi için baş düğümü ve kenar düğümü için adlandırma kuralı hello aşağıda verilmiştir.
   * Baş düğüm`CLUSTERNAME-ssh.azurehdinsight.net`
   * Kenar düğümüne`CLUSTERNAME-ed-ssh.azurehdinsight.net` 

2. 1. adımda sağlanan hello adlandırma desenini kullanarak hello kümesinin hello kenar düğümüne içine SSH. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Bağlandıktan sonra kök kullanıcının hello kümede haline gelir. Merhaba SSH oturumunda hello aşağıdaki komutu kullanın:

        sudo su -

4. Merhaba özel komut dosyası tooinstall Rstudio'dan indirin. Merhaba aşağıdaki komutu kullanın:

        wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/InstallRStudio.sh

5. Merhaba özel komut dosyası Hello izinlerini değiştirin ve hello komut dosyasını çalıştırın. Merhaba aşağıdaki komutları kullanın:

        chmod 755 InstallRStudio.sh
        ./InstallRStudio.sh

6. R Server ile bir Hdınsight kümesi oluştururken bir SSH parola kullandıysanız, bu adımı atlayın ve toohello sonraki devam edin. Bir SSH anahtarı toocreate hello küme yerine kullandıysanız, SSH kullanıcı için bir parola ayarlamanız gerekir. Bu parolayı tooRStudio bağlanırken gerekir. Merhaba aşağıdaki komutları çalıştırın:

        passwd USERNAME
        Current Kerberos password:
        New password:
        Retype new password:
        Current Kerberos password:


7. İstendiğinde **geçerli Kerberos Parola**, basın **ENTER**.  Değiştirmeniz gereken Not `USERNAME` Hdınsight kümenizle bir SSH kullanıcıyla. Parolanızı başarıyla ayarlarsanız, iletiden hello görmeniz gerekir:

        passwd: password updated successfully

    Merhaba SSH oturumu çıkın.

8. Eşleme tarafından bir SSH tünel toohello kümesi oluşturmayı `ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` toohello istemci makine üzerinde hello Hdınsight küme. Yeni bir tarayıcı oturum açmadan önce bir SSH tüneli oluşturmanız gerekir.

   * Linux istemci veya bir Windows İstemcisi ile [Cygwin](http://www.redhat.com/services/custom/cygwin/), bir terminal oturumu açın ve hello aşağıdaki komutu kullanın:

             ssh -L localhost:8787:localhost:8787 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

       Değiştir **kullanıcı adı** Hdınsight kümesi ve değiştirmek için bir SSH kullanıcıyla **CLUSTERNAME** Hdınsight kümenize hello adı.
       Ayrıca bir parola yerine bir SSH anahtarı ekleyerek kullanabileceğiniz `-i id_rsa_key`.        
   * Windows İstemcisi ile PuTTY sonra kullanıyorsanız

     1. Putty'yi açın ve bağlantı bilgilerinizi girin.
     2. Merhaba, **kategori** bölüm toohello sol hello iletişim, genişletin **bağlantı**, genişletin **SSH**ve ardından **tüneller**.
     3. Merhaba üzerinde aşağıdaki bilgilerle hello sağlamak **SSH denetleme seçenekleri bağlantı noktası iletme** form:

        * **Kaynak bağlantı noktası** -hello hello istemci tooforward istediğiniz bağlantı noktası. Örneğin, **8787**.
        * **Hedef** - hello olmalıdır hedef toohello yerel istemci makine eşlenmiş. Örneğin, **localhost:8787**.

            ![SSH tüneli oluşturma](./media/hdinsight-hadoop-r-server-install-r-studio/createsshtunnel.png "SSH tüneli oluşturma")

     4. Tıklatın **Ekle** tooadd hello ayarları ve ardından **açık** tooopen bir SSH bağlantısı.
     5. İstendiğinde, toohello sunucu tooestablish SSH oturumu ve etkinleştir hello tüneli oturum açın.

9. Bir web tarayıcısı açın ve hello bağlantı noktası için hello tünel girdiğiniz temel URL aşağıdaki hello girin:

        http://localhost:8787/ 

10. İstendiğinde tooenter hello SSH kullanıcı adı ve parola tooconnect toohello küme var. Merhaba küme oluştururken bir SSH anahtarı kullandıysanız, 5. adımda oluşturduğunuz hello parola girmeniz gerekir.

    ![TooR Studio bağlanmak](./media/hdinsight-hadoop-r-server-install-r-studio/connecttostudio.png "SSH tüneli oluşturma")

11. tootest hello Rstudio'dan yükleme başarılı olup olmadığını R tabanlı MapReduce ve Spark işlerinin hello kümesinde yürütülür bir test betiğini çalıştırabilirsiniz. toodownload hello test betik toorun Rstudio'dan içinde toohello SSH konsol geri dönün ve aşağıdaki komutları hello girin:

    *    R ile Hadoop kümesi oluşturduysanız, bu komutu kullanın:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi.r
    *    R ile Spark kümesi oluşturduysanız, bu komutu kullanın:

            wget http://mrsactionscripts.blob.core.windows.net/rstudio-server-community-v01/testhdi_spark.r

12. Rstudio'dan içinde indirdiğiniz betiğini sınamak hello bakın. Hello hello dosyasının içeriğini seçin ve ardından hello dosya tooopen çift **çalıştırmak**. Merhaba hello çıktısında görmelisiniz **konsol** bölmesi:

   ![Test hello yükleme](./media/hdinsight-hadoop-r-server-install-r-studio/test-r-script.png "Test hello yükleme")

Başka bir seçenek tootype olabilir `source(testhdi.r)` veya `source(testhdi_spark.r)` tooexecute hello komut dosyası.

## <a name="see-also"></a>Ayrıca bkz.

* [Hdınsight kümelerinde R Server için içerik seçeneklerini işlem](hdinsight-hadoop-r-server-compute-contexts.md)
* [HDInsight üzerinde R Server için Azure Depolama seçenekleri](hdinsight-hadoop-r-server-storage.md)

