---
title: "Windows tabanlı Hdınsight - Azure ile Tez UI aaaUse | Microsoft Docs"
description: "Windows tabanlı Hdınsight Hdınsight'ta nasıl toouse hello Tez UI toodebug Tez işleri öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Windows tabanlı Hdınsight üzerinde Hello Tez UI toodebug Tez işlerinde kullanın
Merhaba Tez UI hello yürütme altyapısı Windows tabanlı Hdınsight kümelerinde olarak Tez kullanan kullanılan toounderstand ve hata ayıklama işleri olabilecek bir web sayfasıdır. bir grafik bağlı öğelerinin her öğenin ayrıntısına ve istatistikleri ve günlük kaydı bilgilerini almak gibi hello Tez UI toovisualize hello iş sağlar.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Windows kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Ön koşullar
* Bir Windows tabanlı Hdınsight kümesi. Yeni küme oluşturma adımları için bkz: [Windows tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Merhaba Tez UI yalnızca 8 Şubat 2016 sonrasında oluşturulan Windows tabanlı Hdınsight kümeleri üzerinde kullanılabilir.
  >
  >
* Bir Windows tabanlı uzak masaüstü istemcisi.

## <a name="understanding-tez"></a>Tez anlama
Tez geleneksel MapReduce işleme büyük hızlarından sağlayan hadoop'ta veri işleme için genişletilebilir bir çerçevedir. Windows tabanlı Hdınsight kümeleri için komutu aşağıdaki Hive sorgunuzu bir parçası olarak hello kullanarak Hive için etkinleştirebilirsiniz bir isteğe bağlı altyapısıdır:

    set hive.execution.engine=tez;

İş gönderilen tooTez olduğunda, yönlendirilmiş Çevrimsiz grafik (hello yürütme hello iş tarafından gerekli hello eylemlerin sırasını açıklayan DAG) oluşturur. Tek tek Eylemler köşeleri olarak adlandırılır ve hello parçası yürütmek genel işi. Merhaba gerçek yürütme hello iş köşe tarafından tanımlanan bir görev çağrılır ve hello kümedeki birden çok düğüm arasında dağıtılmış.

### <a name="understanding-hello-tez-ui"></a>Anlama hello Tez kullanıcı Arabirimi
Merhaba Tez UI Tez kullanma, çalışmakta olan veya sahip işlemler hakkında bilgi daha önce çalışan bir web sayfası sağlar ' dir. Tooview hello Tez tarafından oluşturulan DAG tanır kümeler arasında nasıl dağıtıldığını sayaçları görevleri ve köşeleri ve hata bilgilerini tarafından kullanılan bellek gibi. Aşağıdaki senaryolar hello yararlı bilgiler teklif edebilir:

* Uzun süre çalışan işlemleri görüntüleme, izleme harita ilerlemesini hello ve görevleri azaltır.
* Başarılı veya başarısız işlemler toolearn ilişkin geçmiş verileri analiz etme işleme nasıl geliştirilmiş veya neden başarısız oldu.

## <a name="generate-a-dag"></a>Bir DAG oluştur
kullanan bir iş altyapısı şu anda çalışıyor veya sahip hello son çalıştırılan edilmiş Tez hello varsa hello Tez UI yalnızca veri içermez. Basit Hive sorguları genellikle Tez, yapan filtreleme, gruplama, sıralama, birleşimler, vb. Tez genellikle gerektirir ancak daha karmaşık sorgular kullanmadan çözülebilir.

Aşağıdaki adımları toorun Tez kullanma yürütecek bir Hive sorgusu hello kullanın.

1. Toohttps://CLUSTERNAME.azurehdinsight.net, bir web tarayıcısında gidin nerede **CLUSTERNAME** Hdınsight kümenize hello adıdır.
2. Merhaba hello sayfanın üst kısmındaki hello Hello menüsünden seçin **Hive Düzenleyicisi**. Bu örnek sorgu aşağıdaki hello ile bir sayfa görüntülenir.

        Select * from hivesampletable

    Merhaba örnek sorgu silebilir ve hello şununla değiştirin.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Select hello **gönderme** düğmesi. Merhaba **proje oturumunu** hello sayfanın hello kısmına hello sorgu hello durumunu görüntüler. Bir kez durum değişikliklerini çok hello**tamamlandı**seçin hello **ayrıntıları görüntüle** bağlantı tooview hello sonuçları. Merhaba **iş çıktısı** benzer toohello aşağıdaki gibi olmalıdır:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Merhaba Tez UI kullanın
> [!NOTE]
> Uzak Masaüstü tooconnect toohello baş düğümler kullanmalısınız hello Tez UI yalnızca hello küme baş düğümü hello masaüstünden kullanılabilir.
>
>

1. Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin. Merhaba Hdınsight dikey penceresinde Hello üstten hello seçin **Uzak Masaüstü** simgesi. Bu hello Uzak Masaüstü dikey penceresinde görüntülenir

    ![Uzak Masaüstü simgesi](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. Merhaba Uzak Masaüstü dikey penceresinden seçin **Bağlan** tooconnect toohello küme baş düğümüne. İstendiğinde, hello küme Uzak Masaüstü kullanıcı adı ve parola tooauthenticate hello bağlantısı kullanın.

    ![Uzak Masaüstü Bağlantısı simgesi](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Uzak Masaüstü bağlantısı etkin değil, bir kullanıcı adı, parola ve sona erme tarihi sağlayın, sonra seçin **etkinleştirmek** tooenable Uzak Masaüstü. Etkinleştirildikten sonra hello önceki adımları tooconnect kullanın.
   >
   >
3. Bağlantı kurulduktan sonra hello Uzak Masaüstü, select hello dişli simgesine hello sağ üst tarafındaki hello tarayıcı, Internet Explorer'ı açın ve ardından **Uyumluluk Görünümü Ayarları**.
4. Merhaba altından **Uyumluluk Görünümü Ayarları**temizleyin hello onay kutusunu **görüntüleme intranet sitelerini Uyumluluk Görünümü'nde** ve **kullanım Microsoft Uyumluluk listeleri**, ve ardından **Kapat**.
5. Internet Explorer'da toohttp://headnodehost:8188 Gözat/tezui / #/. Bu hello Tez kullanıcı Arabirimi görüntüler

    ![Tez kullanıcı Arabirimi](./media/hdinsight-debug-tez-ui/tezui.png)

    Merhaba Tez UI yüklediğinde, çalışmakta olan ya da silinmiş Dag'leri listesini hello küme üzerinde çalışan görürsünüz. Merhaba Dag adı, kimliği, gönderen, durumu, başlangıç saati, bitiş zamanı, süresi, uygulama kimliği ve kuyruk Hello varsayılan görünümü içerir. Daha fazla sütun hello sayfasının sağ hello hello dişli simgesini kullanarak eklenebilir.

    Yalnızca bir giriş varsa, önceki bölümde hello çalıştırdığınız hello sorgu için olacaktır. Birden çok girdi varsa, arama hello Dag'leri yukarıda hello alanlarında arama ölçütü girerek, ardından isabet **Enter**.
6. Select hello **Dag adı** hello en son DAG girişi. Bu hello seçeneği toodownload hello DAG hakkında bilgi içeren JSON dosyaları zip yanı sıra hello DAG hakkında bilgi görüntüler.

    ![DAG ayrıntıları](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Merhaba yukarıda **DAG ayrıntıları** hello DAG kullanılan toodisplay bilgilerini olabilir birkaç bağlantılardır.

   * **DAG sayaçları** bu DAG sayaçları bilgilerini görüntüler.
   * **Grafik görünümü** bu DAG grafik gösterimi görüntüler.
   * **Tüm köşeleri** bu DAG hello köşeleri listesini görüntüler.
   * **Tüm Görevler** bu DAG tüm köşeleri hello görevlerde listesini görüntüler.
   * **Tüm TaskAttempts** hello hakkında bilgi görüntüler toorun görevler için bu DAG çalışır.

     > [!NOTE]
     > Merhaba sütun görüntü köşeleri, görevleri ve TaskAttempts kaydırırsanız olduğuna dikkat edin tooview bağlantıları **sayaçları** ve **görüntülemek veya günlükleri indirmek** her satır için.
     >
     >

     Merhaba işlemiyle hatası varsa, hello DAG ayrıntıları hello başarısız görev hakkında bağlantılar tooinformation birlikte başarısız oldu, durumunu görüntüler. Tanılama bilgileri hello DAG Ayrıntılar altında görüntülenir.
8. Seçin **grafik görünümü**. Bu grafik gösterimi hello DAG görüntüler. Merhaba görünüm toodisplay bilgi ilgili her köşe üzerinden hello fare yerleştirebilirsiniz.

    ![Grafik görünümü](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Bir köşe tıklatarak hello yükler **köşe ayrıntıları** bu öğe için. Tıklatın hello üzerinde **harita 1** köşe toodisplay ayrıntılar bu öğe için. Seçin **Onayla** tooconfirm hello gezinti.

    ![Köşe ayrıntıları](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Şimdi ilgili toovertices ve görevleri bağlantıları hello sayfanın üst kısmındaki hello gerektiğini unutmayın.

    > [!NOTE]
    > Bu sayfaya geri çok giderek de ulaşması**DAG ayrıntıları**, seçme **köşe ayrıntıları**ve ardından hello seçerek **harita 1** köşe.
    >
    >

    * **Köşe sayaçları** bu köşe sayaç bilgilerini görüntüler.
    * **Görevleri** bu köşe için görevleri görüntüler.
    * **Görev denemeleri** bu köşe için deneme toorun görevler hakkındaki bilgileri görüntüler.
    * **Kaynakları & iç havuzlar** bu köşe için iç havuzlar ve veri kaynakları görüntüler.

      > [!NOTE]
      > Merhaba önceki menüsüyle hello sütun görüntü görevler için kaydırabilirsiniz gibi görev denemeleri ve kaynakları & Sinks__ toodisplay toomore bilgileri her öğe için bağlar.
      >
      >
11. Seçin **görevleri**, ve select hello öğesi adlı **00_000000**. Bu görüntüler **görev ayrıntıları** bu görev için. Bu ekranda görüntüleyebileceğiniz **görev sayaçları** ve **görev denemeleri**.

    ![Görev Ayrıntıları](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Sonraki Adımlar
Toouse hello Tez nasıl görüntüleyebilirim öğrendiniz, daha fazla bilgi edinmek [hdınsight'ta Hive kullanarak](hdinsight-use-hive.md).

Daha ayrıntılı Tez teknik bilgi için bkz: Merhaba [Hortonworks Tez sayfanın](http://hortonworks.com/hadoop/tez/).
