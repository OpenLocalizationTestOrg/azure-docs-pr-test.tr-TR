---
title: "aaaMonitor ve Azure Hdınsight Ambari Web kullanıcı arabirimini kullanarak yönetme | Microsoft Docs"
description: "Bilgi nasıl toouse Ambari toomonitor ve Linux tabanlı Hdınsight kümelerini yönetme. Bu belgede nasıl toouse hello Ambari Web kullanıcı arabirimini Hdınsight ile dahil kümeleri öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Merhaba Ambari Web kullanıcı arabirimini kullanarak Hdınsight kümelerini yönetme

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari hello yönetimi ve Hadoop kümesi kolay toouse web kullanıcı Arabirimi ve REST API'si sağlayarak izlemenin basitleştirir. Ambari Linux tabanlı Hdınsight kümelerine dahil ve kullanılan toomonitor hello olan küme yapılandırması değişiklikler yapın.

Bu belgede nasıl toouse hello Ambari Web kullanıcı Arabirimi bir Hdınsight kümesini öğrenin.

## <a id="whatis"></a>Ambari nedir?

[Apache Ambari](http://ambari.apache.org) kullanımı kolay web kullanıcı Arabirimi sağlayarak Hadoop yönetimini basitleştirir. Ambari kullanabileceğiniz oluşturmak, yönetmek ve Hadoop kümelerini izleme. Geliştiriciler tümleştirebilir Bu yetenekler uygulamalarına hello kullanarak [Ambari REST API'leri](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Merhaba Ambari Web kullanıcı Arabirimi, varsayılan olarak hello Linux işletim sistemi kullanmak Hdınsight kümeleri ile sağlanır.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). 

## <a name="connectivity"></a>Bağlantı

Merhaba Ambari Web kullanıcı Arabirimi, HTTPS://CLUSTERNAME.azurehdidnsight.net, konumunda Hdınsight kümenize kullanılabilir olduğu **CLUSTERNAME** hello kümenizin adıdır.

> [!IMPORTANT]
> Hdınsight üzerinde tooAmbari bağlanırken HTTPS gerektirir. Kimlik doğrulaması için istendiğinde hello Yönetici hesap adı ve parola hello küme oluştururken verdiğiniz kullanın.

## <a name="ssh-tunnel-proxy"></a>SSH tüneli (proxy)

Kümeniz için Ambari hello doğrudan Internet erişilebilir olsa da, bazı Ambari Web kullanıcı Arabirimi (örneğin, toohello Jobtracker'a) üzerinde gösterilmez hello bağlantılarından Internet hello. Bu hizmetleri tooaccess SSH tüneli oluşturmanız gerekir. Daha fazla bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Ambari Web kullanıcı Arabirimi

Toohello Ambari Web kullanıcı arabirimini bağlanırken istendiğinde tooauthenticate toohello sayfa görünüyor. Merhaba küme yönetici kullanıcı (varsayılan Yönetici) ve küme oluşturma sırasında kullanılan parola kullanın.

Başlangıç sayfası açıldığında, hello çubuğu hello üstünde unutmayın. Bu çubuğu hello aşağıdakileri içeren bilgileri ve denetimleri:

![ambari nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Ambari logosu** -açılır hello Pano kullanılan toomonitor hello kümesi olabilir.

* **Küme adı # ops** -devam eden ambarı işlemler hello sayısını görüntüler. Seçme hello küme adı veya **# ops** arka plan işlemleri listesini görüntüler.

* **# Uyarıları** -görüntüler uyarı veya kritik uyarı durumunda hello küme.

* **Pano** -görüntüler hello Pano.

* **Hizmetleri** -hello kümedeki hello Hizmetleri için bilgi ve yapılandırma ayarları.

* **Ana bilgisayar** -hello küme hello düğümler için bilgileri ve yapılandırma ayarları.

* **Uyarıları** -günlük bilgi, uyarı ve kritik uyarılar.

* **Yönetici** -hello küme, hizmet hesabı bilgilerini ve Kerberos güvenlik yüklü yazılım yığını/Hizmetleri.

* **Yönetici düğmesi** -ambarı yönetimi, kullanıcı ayarlarını ve oturum kapatma.

## <a name="monitoring"></a>İzleme

### <a name="alerts"></a>Uyarılar

Merhaba aşağıdaki listede hello ortak uyarı durumları Ambari tarafından kullanılan içerir:

* **TAMAM**
* **Uyarı**
* **KRİTİK**
* **BİLİNMEYEN**

Dışındaki uyarıları **Tamam** hello neden **# uyarıları** girişi hello üstünde hello sayfa toodisplay hello uyarı sayısı. Bu girdi seçerek hello uyarıları ve bunların durumunu görüntüler.

Uyarıları hello görüntülenebilir birkaç varsayılan gruplar halinde düzenlenir **uyarıları** sayfası.

![Uyarılar sayfası](./media/hdinsight-hadoop-manage-ambari/alerts.png)

Merhaba grupları hello kullanarak yönetebileceğiniz **Eylemler** menü ve seçerek **uyarı grupları yönet**.

![Uyarı gruplar iletişim yönetme](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

Ayrıca, uyarı yöntemleri yönetmek ve uyarı bildirimleri hello oluşturabilirsiniz **Eylemler** seçerek menü __yönetmek uyarı bildirimleri__. Geçerli herhangi bir bildirim görüntülenir. Ayrıca, buradan bildirimler de oluşturabilirsiniz. Bildirimler, üzerinden gönderilebilir **e-posta** veya **SNMP** belirli uyarı önem birleşimleri olduğunda. Örneğin, bir e-posta iletisi hello uyarıların hiçbirini zaman hello gönderebilirsiniz **YARN varsayılan** grubunu çok Ayarla**kritik**.

![Uyarı iletişim kutusu oluşturma](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Son olarak, seçme __uyarı ayarlarını Yönet__ hello gelen __Eylemler__ menü tooset hello kaç kez bir uyarı gerekir görünmesi bir bildirim gönderilmeden önce sağlar. Bu ayar, geçici hataları için kullanılan tooprevent bildirimleri olabilir.

### <a name="cluster"></a>Küme

Merhaba **ölçümleri** hello Pano sekmesi kolay toomonitor hello kümenizi durumunu bir bakışta olun pencere öğeleri, bir dizi içerir. Birkaç pencere öğeleri gibi **CPU kullanımı**, tıklatıldığında ek bilgileri sağlayın.

![Pano ölçümlerle](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Merhaba **Heatmaps** sekmesi ölçümleri yeşil toored giderek renkli heatmaps olarak görüntüler.

![Pano heatmaps ile](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Merhaba kümede hello düğüm üzerinde daha fazla bilgi için seçin **ana**. Daha sonra ilgilendiğiniz hello belirli düğümünü seçin.

![ana bilgisayar ayrıntıları](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Hizmetler

Merhaba **Hizmetleri** kenar hello Panoda hello hello kümede çalışan hello hizmetlerinin durumunu hızlı fikir sağlar. Çeşitli simgeler kullanılan tooindicate durumu veya alınması gereken eylemler olacaktır. Örneğin, bir hizmet geri dönüşüm toobe gerekiyorsa sarı geri dönüşüm simgesi görüntülenir.

![Hizmetleri yan çubuğu](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> Görüntülenen hello Hizmetleri Hdınsight küme türleri ve sürümleri arasında farklılık gösterir. Burada görüntülenen hello Hizmetleri kümeniz için görüntülenen hello Hizmetleri farklı olabilir.

Bir hizmet seçmeden hello hizmette daha ayrıntılı bilgiler görüntüler.

![Hizmet özet bilgileri](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Hızlı bağlantılar

Bazı Hizmetleri görünen bir **hızlı bağlantılar** hello sayfanın üst kısmındaki hello bağlantı. Bu kullanılan tooaccess hizmete özgü web Uı'lar, aşağıdaki gibi olabilir:

* **İş Geçmişi** -MapReduce iş geçmişi.
* **Resource Manager** -YARN ResourceManager UI.
* **İş** -Hadoop dağıtılmış dosya sistemi (HDFS) iş UI.
* **Oozie Web kullanıcı Arabirimi** -Oozie UI.

Aşağıdaki bağlantılardan birini seçerek yeni bir sekme hello seçili sayfasını görüntüler, tarayıcıda açılır.

> [!NOTE]
> Seçme hello **hızlı bağlantılar** girişi bir hizmet için "Sunucu bulunamadı" hata döndürebilir. Bu hatayla karşılaşırsanız, hello kullanırken SSH tüneli kullanmalısınız **hızlı bağlantılar** bu hizmet için girişi. Bilgi için bkz: [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md)

## <a name="management"></a>Yönetim

### <a name="ambari-users-groups-and-permissions"></a>Ambari kullanıcılar, gruplar ve izinler

Kullanıcılar, gruplar ve izinler ile çalışma kullanılırken desteklenir bir [etki alanına katılmış](hdinsight-domain-joined-introduction.md) Hdınsight kümesi. Etki alanına katılmış bir kümede hello ambarı Yönetimi kullanıcı arabirimini kullanma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> Linux tabanlı Hdınsight kümenizdeki hello Ambari izleme (hdinsightwatchdog) Hello parolasını değiştirmeyin. Merhaba parola sonları değiştirme özelliği toouse betik eylemleri hello veya kümeniz ile ölçeklendirme işlemleri gerçekleştirin.

### <a name="hosts"></a>Ana bilgisayarlar

Merhaba **ana** sayfası hello kümedeki tüm konaklarda listeler. toomanage ana bilgisayarlar, aşağıdaki adımları izleyin.

![ana sayfa](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> Ekleme, yetkisini alma ve bir ana bilgisayar recommissioning Hdınsight kümeleri ile kullanılmamalıdır.

1. Toomanage istediğiniz hello konağı seçin.

2. Kullanım hello **Eylemler** menü tooselect hello eylem tooperform istiyor:

   * **Tüm bileşenleri başlatın** -hello konakta tüm bileşenleri başlatın.

   * **Tüm bileşenleri Durdur** -hello konakta tüm bileşenleri durdurun.

   * **Tüm bileşenleri yeniden** - Dur ve tüm bileşenleri hello konakta başlatın.

   * **Bakım modunu açmak** -hello ana bilgisayar için uyarıları bastırır. Uyarıları oluşturan eylemleri gerçekleştiriyorsanız Bu mod etkinleştirilmelidir. Örneğin, bir Hizmeti'ni durdurma ve başlatma.

   * **Bakım modunu devre dışı bırakmak** -döndürür hello konak toonormal uyarı.

   * **Durdur** -durakları DataNode veya hello ana bilgisayarda NodeManagers.

   * **Başlat** -DataNode başlatır veya hello ana bilgisayarda NodeManagers.

   * **Yeniden** -durur ve hello ana bilgisayarda DataNode veya NodeManagers başlatır.

   * **Yetkisini** -hello kümeden bir ana bilgisayarı kaldırır.

     > [!NOTE]
     > Bu eylem, Hdınsight kümelerinde kullanmayın.

   * **Recommission** -daha önce yetkisi alınmış konak toohello kümesi ekler.

     > [!NOTE]
     > Bu eylem, Hdınsight kümelerinde kullanmayın.

### <a id="service"></a>Hizmetleri

Merhaba gelen **Pano** veya **Hizmetleri** sayfasında, hello kullanın **Eylemler** düğme services toostop hello listesi hello altındaki ve tüm hizmetleri başlatın.

![Hizmet eylemleri](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Sırada **Hizmet Ekle** listelenen bu menüde, kullanılan tooadd Hizmetleri toohello Hdınsight kümesi olmamalıdır. Küme hazırlama sırasında bir betik eylemi kullanarak yeni hizmetlerin eklenmesi gerekir. Betik eylemleri kullanma hakkında daha fazla bilgi için bkz: [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](hdinsight-hadoop-customize-cluster-linux.md).

Merhaba sırasında **Eylemler** düğmesi tüm hizmetleri yeniden başlatın, genellikle toostart, Dur veya yeniden başlatma belirli bir hizmet istiyor. Bireysel bir hizmet adımları tooperform eylemleri aşağıdaki hello kullan:

1. Merhaba gelen **Pano** veya **Hizmetleri** sayfasında, bir hizmet seçin.

2. Merhaba, hello üstten **Özet** sekmesinde, hello kullan **hizmet eylemleri** düğmesi ve select hello eylem tootake. Bu, tüm düğümlerde hello hizmetini yeniden başlatır.

    ![hizmet eylemi](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Merhaba küme çalışırken bazı hizmetleri yeniden uyarılar oluşturabilir. tooavoid uyarıları, hello kullanabileceğiniz **hizmet eylemleri** düğmesini tooenable **Bakım modu** hello yeniden başlatma işlemini gerçekleştirmeden önce hello hizmeti.

3. Bir eylem seçildikten sonra hello **# op** arka plan işlemi gerçekleştirildiği hello sayfa artışlarla tooshow hello üstündeki girişi. Toodisplay yapılandırdıysanız, arka plan işlemleri hello listesi görüntülenir.

   > [!NOTE]
   > Etkinleştirmiş olmanız durumunda **Bakım modu** toodisable hello hizmeti için unutmayın hello kullanarak **hizmet eylemleri** hello işlemi tamamlandıktan sonra düğmesine tıklayın.

bir hizmet tooconfigure hello aşağıdaki adımları kullanın:

1. Merhaba gelen **Pano** veya **Hizmetleri** sayfasında, bir hizmet seçin.

2. Select hello **yapılandırmalar** sekmesini hello geçerli yapılandırması görüntülenir. Önceki yapılandırmaların listesi de görüntülenir.

    ![Yapılandırmaları](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Merhaba görüntülenen alanları toomodify hello yapılandırmasını kullanın ve ardından **kaydetmek**. Veya önceki bir yapılandırma seçin ve ardından **geçerli hale** tooroll toohello önceki ayarlarını yedekleyin.

## <a name="ambari-views"></a>Ambari görünümleri

Ambari görünümleri tooplug kullanıcı Arabirimi öğeleri geliştiriciler Ambari Web kullanıcı arabirimini hello izin hello kullanarak [Ambari görünümleri Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views). Hdınsight Hadoop küme türü görünümlerle aşağıdaki hello sağlar:

* Yarn sıra Yöneticisi: hello sıra yöneticisi görüntüleme ve değiştirme YARN sıraları için basit bir kullanıcı Arabirimi sağlar.

* Hive görünümü: hello Hive görünümü toorun Hive sorguları doğrudan web tarayıcınızdan sağlar. Sorguları Kaydet, sonuçları görüntülemek, toohello küme depolama sonuçları kaydetmek veya sonuçları tooyour yerel sistem indirin. Hive görünümleri kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile kullanım Hive görünümleri](hdinsight-hadoop-use-hive-ambari-view.md).

* Tez görünümü: toobetter sağlar hello Tez görünüm anlamak ve işleri en iyi duruma getirme. Tez işlerinde nasıl yürütülür ve hangi kaynaklara kullanılan bilgileri görüntüleyebilirsiniz.
