---
title: "aaaUse SSH tünel tooaccess Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse bir SSH tünel toosecurely Gözat, Linux tabanlı Hdınsight düğümler üzerinde barındırılan web kaynaklar hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>SSH tünel tooaccess Ambari web kullanıcı Arabirimi, kaynak, iş, Oozie ve diğer web Uı'lar kullanın

Linux tabanlı Hdınsight kümeleri hello Internet üzerinden erişim tooAmbari web kullanıcı Arabirimi sağlar, ancak hello UI özelliklerinden bazıları değildir. Örneğin, hello web kullanıcı Arabirimi Ambari ortaya çıkmış diğer hizmetler için. Merhaba Ambari web kullanıcı Arabirimi tam işlevsellik için bir SSH tünel toohello küme baş kullanmanız gerekir.

## <a name="why-use-an-ssh-tunnel"></a>SSH tüneli neden kullanılır?

Ambari hello menülerde çeşitli yalnızca SSH tüneli çalışır. Bu menüler web siteleri ve alt düğümleri gibi diğer düğüm türleri üzerinde çalışan hizmetleri kullanır. Genellikle, bu web sitelerinin güvenli değildir, güvenli toodirectly sunmaya olmadığı için kendilerine Internet hello.

Web Uı'lar aşağıdaki hello SSH tüneli gerektirir:

* Kaynak
* İş
* İş parçacığı yığınları
* Oozie web kullanıcı Arabirimi
* HBase ana ve günlükleri kullanıcı Arabirimi

Betik eylemleri toocustomize kümenizi kullanırsanız, herhangi bir hizmet veya bir web kullanıcı arabirimini kullanıma yüklediğiniz utilities SSH tüneli gerektirir. Örneğin, bir betik eylemi kullanarak ton yüklerseniz, bir SSH tünel tooaccess hello Hue web kullanıcı arabirimini kullanmanız gerekir.

> [!IMPORTANT]
> Bir sanal ağ üzerinden doğrudan erişim tooHDInsight varsa, toouse SSH tünelleri gerekmez. Merhaba doğrudan Hdınsight aracılığıyla bir sanal ağ erişimini ilişkin bir örnek için bkz: [bağlanmak Hdınsight tooyour şirket içi ağ](connect-on-premises-network.md) belge.

## <a name="what-is-an-ssh-tunnel"></a>SSH tüneli nedir

[Güvenli Kabuk (SSH) tüneli](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) tooa bağlantı yerel iş istasyonunda gönderilen trafiğini yönlendirir. Merhaba trafik bir SSH bağlantısı tooyour Hdınsight küme baş düğümüne yönlendirilir. Merhaba baş düğümünde geldiyse gibi hello isteği çözümlenir. Merhaba yanıt sonra geri hello tünel tooyour iş istasyonu yönlendirilir.

## <a name="prerequisites"></a>Ön koşullar

* Bir SSH istemcisi. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

* Olabilir bir web tarayıcısı toouse SOCKS5 proxy yapılandırılmış.

    > [!WARNING]
    > Windows'da yerleşik hello SOCKS proxy desteği SOCKS5 desteklemez ve bu belgedeki hello adımlara çalışmaz. Hello aşağıdaki tarayıcılardan Windows proxy ayarlarını kullanır ve hello adımları bu belgede çalışmak desteklemez:
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome ayrıca hello Windows proxy ayarlarını kullanır. Ancak, SOCKS5 Destek Uzantıları yükleyebilirsiniz. Öneririz [FoxyProxy standart](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).

## <a name="usessh"></a>Merhaba SSH komutunu kullanarak bir tünel oluşturma

Kullanım hello şu komutu toocreate hello kullanarak SSH tüneli `ssh` komutu. Değiştir **kullanıcı adı** Hdınsight kümesi ve değiştirmek için bir SSH kullanıcıyla **CLUSTERNAME** Hdınsight kümenize hello adı:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Bu komut, SSH üzerinden trafik toolocal bağlantı noktası 9876 toohello küme yönlendiren bir bağlantı oluşturur. Başlangıç seçenekleri şunlardır:

* **D 9876** -hello hello tüneli üzerinden trafiğini yönlendiren yerel bağlantı noktası.
* **C** -web trafiği çoğunlukla metin olduğundan tüm verileri sıkıştırmak.
* **2** -force SSH tootry Protokolü sürüm 2 yalnızca.
* **q** -Sessiz mod.
* **T** -biz yalnızca bir bağlantı noktası iletme beri sözde tty ayırma, devre dışı.
* **n**-STDIN, okunması biz yalnızca bir bağlantı noktası iletme beri engelleyin.
* **N** -biz yalnızca bir bağlantı noktası iletme olduğundan bir uzak komutu yürütülmez.
* **f** -hello arka planda çalıştırın.

Merhaba komut bittikten sonra gönderilen trafiğin tooport 9876 hello yerel bilgisayarda yönlendirilmiş toohello küme baş düğümüne ' dir.

## <a name="useputty"></a>PuTTY kullanarak bir tünel oluşturma

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) Windows için grafik SSH istemcidir. PuTTY kullanarak SSH tüneli adımları toocreate aşağıdaki hello kullan:

1. Putty'yi açın ve bağlantı bilgilerinizi girin. Merhaba PuTTY ile bilmiyorsanız bkz [PuTTY belgeleri (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. Merhaba, **kategori** bölüm toohello sol hello iletişim, genişletin **bağlantı**, genişletin **SSH**ve ardından **tüneller**.

3. Merhaba üzerinde aşağıdaki bilgilerle hello sağlamak **SSH denetleme seçenekleri bağlantı noktası iletme** form:
   
   * **Kaynak bağlantı noktası** -hello hello istemci tooforward istediğiniz bağlantı noktası. Örneğin, **9876**.

   * **Hedef** -hello Linux tabanlı Hdınsight kümesi için SSH adresi hello. Örneğin, **mycluster-ssh.azurehdinsight.net**.

   * **Dinamik** - Dinamik SOCKS proxy yönlendirmesini etkinleştirir.
     
     ![Görüntü seçenekleri tünel](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Tıklatın **Ekle** tooadd hello ayarları ve ardından **açık** tooopen bir SSH bağlantısı.

5. İstendiğinde, toohello Server'da oturum açın.

## <a name="use-hello-tunnel-from-your-browser"></a>Merhaba tünel tarayıcınızdan kullanın

> [!IMPORTANT]
> aynı proxy ayarları tüm platformlarda hello sağladığı gibi hello bu bölümü kullanın hello Mozilla FireFox tarayıcı adımlar. Google Chrome gibi modern tarayıcılar uzantı hello tünel ile FoxyProxy toowork gibi gerektirebilir.

1. Merhaba tarayıcı toouse yapılandırma **localhost** ve ne zaman kullanılan başlangıç bağlantı noktası olarak hello tünel oluşturma bir **SOCKS v5** proxy. İşte hello Firefox ayarlarını gibi arayın. Farklı bir bağlantı noktasıyla 9876 kullandıysanız, başlangıç bağlantı noktası toohello hangisini kullanılan değiştirin:
   
    ![Firefox ayarlarının görüntüsü](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > Seçme **uzak DNS** hello Hdınsight kümesi kullanarak etki alanı adı sistemi (DNS) isteklerinin giderir. Bu ayar hello küme baş düğümüne hello kullanarak DNS çözümler.

2. Merhaba tünel çalıştığını gibi bir siteyi ziyaret ederek doğrula [http://www.whatismyip.com/](http://www.whatismyip.com/). Merhaba IP bir hello Microsoft Azure veri merkezi tarafından kullanılması gereken döndürdü.

## <a name="verify-with-ambari-web-ui"></a>Ambari web kullanıcı Arabirimi ile doğrulayın

Merhaba küme kurulduktan sonra hello Ambari Web hizmeti web Uı'lar erişebilirsiniz adımları tooverify aşağıdaki hello kullanın:

1. Tarayıcınızda, toohttp://headnodehost:8080 gidin. Merhaba `headnodehost` adresi hello tünel toohello küme gönderilir ve ambarı üzerinde çalıştığı toohello headnode çözümleyin. İstendiğinde, kümeniz için hello yönetici kullanıcı adı (Yönetici) ve parola girin. Merhaba Ambari web kullanıcı Arabirimi tarafından ikinci kez istenebilir. Bu durumda, hello bilgileri yeniden girin.

   > [!NOTE]
   > Merhaba http://headnodehost:8080 adresi tooconnect toohello küme kullanırken hello tünelinden bağlanırsınız. İletişim HTTPS yerine hello SSH tüneli kullanılarak güvenli hale getirilir. tooconnect üzerinde HTTPS kullanarak Internet Merhaba, https://CLUSTERNAME.azurehdinsight.net, kullanın nerede **CLUSTERNAME** hello küme hello adıdır.

2. Ambari Web kullanıcı arabirimini Hello HDFS hello sayfasının hello soldaki hello listeden seçin.

    ![Seçili HDFS görüntüsüyle](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Merhaba HDFS hizmet bilgileri görüntülendiğinde seçin **hızlı bağlantılar**. Merhaba küme baş düğümler listesi görüntülenir. Merhaba baş düğümler birini seçin ve ardından **iş UI**.

    ![Görüntü hello QuickLinks menüsü ile genişletilmiş](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Seçtiğinizde, __hızlı bağlantılar__, bekleme göstergesi alabilirsiniz. Yavaş bir internet bağlantınız varsa, bu durum oluşabilir. Bir veya iki hello sunucudan alınan hello veri toobe için dakika bekleyin ve sonra hello listesi tekrar deneyin.
   >
   > Merhaba, bazı girişler **hızlı bağlantılar** menü hello ekranın sağ tarafında hello tarafından kesilmiş. Bu durumda, farenizi kullanarak hello menüsünü genişletin ve hello sağ ok anahtar tooscroll hello ekran toohello sağ toosee hello geri kalanı hello menüsünü kullanın.

4. Aşağıdaki görüntü bir sayfa benzer toohello görüntülenir:

    ![Merhaba iş UI görüntüsü](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Bu sayfa için Hello URL dikkat edin. çok benzer olmalıdır**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/küme**. Bu URI hello iç hello düğümün tam etki alanı adı (FQDN) kullanıyor ve SSH tüneli kullanırken, yalnızca erişilebilir.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toocreate ve kullanım SSH tüneli bkz belge diğer yolları toouse Ambari için aşağıdaki hello öğrendiğinize göre:

* [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)

Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

