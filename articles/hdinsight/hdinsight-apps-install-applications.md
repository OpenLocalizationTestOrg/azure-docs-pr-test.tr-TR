---
title: "Azure hdınsight'ta aaaInstall üçüncü taraf Hadoop uygulamaları | Microsoft Docs"
description: "Bilgi nasıl tooinstall üçüncü taraf Hadoop uygulamaları Azure hdınsight'ta."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Azure HDInsight'a üçüncü taraf Hadoop uygulamaları yükleme

Bu makalede, bilgi nasıl tooinstall zaten yayımlanmış bir üçüncü taraf Hadoop uygulama Azure Hdınsight üzerinde. Kendi uygulamanızı yükleme yönergeleri için bkz. [Özel HDInsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md).

HDInsight uygulaması kullanıcıların Linux tabanlı HDInsight kümesine yükleyebileceği bir uygulamadır. Bu uygulamalar Microsoft veya bağımsız yazılım satıcıları (ISV) tarafından ya da sizin tarafınızdan geliştirilebilir.  

Şu anda, yayımlanmış dört uygulama vardır:

* **Hdınsight üzerinde DATAIKU DDS**: Dataiku DSS (veri bilimi Studio) olan veri sağlayan bir yazılım uzmanları (veri bilimcilerine, iş analistleri, geliştiricilerin...) tooprototype, derleme ve raw veri dönüştürme yüksek oranda belirli hizmetleri dağıtma etkili iş tahminleri.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) etkileşimli şekilde toodiscover analistleri sunar çözümlemek ve büyük veri üzerinde hello sonuçları görselleştirebilirsiniz. Ek veri kaynaklarını kolayca toodiscover yeni ilişkiler çekmek ve ihtiyaç hello yanıtlar alın.
* **Streamsets veri toplayıcı HDnsight için** , tasarlamak, test, dağıtma ve any herhangi yönetmenizi akış ve toplu veri kafes ardışık düzen alma ve çeşitli dahil bir tam özellikli tümleşik geliştirme ortamı (IDE) sağlar Akış dönüşümleri — toowrite özel kod kalmadan tüm. 
* **Hdınsight için CDAP cask** hello ilk birleşik hello zaman tooproduction veri uygulamaları ve verileri Göller için aşağı % 80'keser büyük veri tümleştirme platformu sağlar. Bu uygulama yalnızca Standart HBase 3.4 kümelerini destekler.
* **Hdınsight (Beta) için H2O yapay zeka** H2O Sparkling su dağıtılmış algoritmalarını aşağıdaki hello destekler: GLM, Naïve Bayes, dağıtılmış rasgele orman, gradyan artırmanın makine, derin sinir ağları, derin, K-ortalamaları, PCA, öğrenme Genelleştirilmiş düşük sıra modelleri, Anomali algılama ve Autoencoders.
* **Kyligence analiz platformu** Kyligence analizi Platformu (KAP) Apache Kylin ve Apache Hadoop tarafından desteklenen bir kurumsal kullanıma hazır veri ambarı; büyük ölçekli veri kümesi üzerinde saniyeden sorgu gecikmesi güçlendirir ve veri analizi için işletme kullanıcılarının ve analistleri basitleştirir. 
* **SnapLogic Hadooplex** hello SnapLogic Hdınsight üzerinde çalışan Hadooplex müşteriler tooget toobusiness Öngörüler daha hızlı Self Servis veri alımı ve neredeyse tüm kaynak toohello Microsoft Azure bulut hazırlık sağlayarak sağlar Platform.
* **KNIME Spark Yürütücü için Spark iş sunucusu** KNIME Spark Yürütücü için Spark iş sunucusu olan kullanılan tooconnect hello KNIME analiz platformu tooHDInsight kümeleri.

Bu makalede sağlanan hello yönergeler Azure portalını kullanın. Ayrıca hello portalından hello Azure Resource Manager şablonu aktarma veya satıcılardan hello Resource Manager şablonunun bir kopyasını alın ve Azure PowerShell ve Azure CLI toodeploy hello şablonu kullanabilirsiniz.  Bkz. [HDInsight’ta Resource Manager şablonları kullanarak Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Ön koşullar
Mevcut bir Hdınsight kümesine Hdınsight uygulamalarını tooinstall istiyorsanız bir Hdınsight kümesi olması gerekir. toocreate biri bkz [küme oluşturma](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). HDInsight uygulamalarını ayrıca bir HDInsight kümesi oluştururken yükleyebilirsiniz.

## <a name="install-applications-tooexisting-clusters"></a>Uygulamaları tooexisting kümeleri yükleyin
Merhaba aşağıdaki yordamda nasıl gösterilmektedir tooinstall Hdınsight uygulamaları tooan varolan Hdınsight kümesi.

**tooinstall Hdınsight uygulaması**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello soldaki menüde.  Bu seçeneği görmüyorsanız **Diğer Hizmetler** ve ardından **HDInsight Kümeleri**’ne tıklayın.
3. Bir HDInsight kümesine tıklayın.  Henüz yoksa öncelikle bir tane oluşturmanız gerekir.  bkz. [Küme oluşturma](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Tıklatın **uygulamaları** hello altında **yapılandırmaları** kategorisi. Yüklü uygulamaların bir listesini görebilirsiniz. Uygulamaları bulamazsanız, bu sürümü hello Hdınsight kümesi için hiçbir uygulamaları yok anlamına gelir.
   
    ![HDInsight uygulamaları portal menüsü](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Tıklatın **Ekle** hello dikey Pencere menüsünden. 
   
    ![HDInsight uygulamaları yüklü uygulamalar](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Mevcut HDInsight uygulamalarının listesini görebilirsiniz.
   
    ![HDInsight uygulamaları kullanılabilir uygulamalar](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Merhaba uygulamalardan birine tıklayın, hello yasal koşulları kabul edin ve ardından **seçin**.

Merhaba portal bildirimleri hello yükleme durumunu görebilirsiniz (Merhaba portal hello üstündeki hello zil simgesine tıklayın). Merhaba sonra Merhaba uygulaması hello yüklü uygulamalar dikey penceresinde görünür uygulama yüklenir.

## <a name="install-applications-during-cluster-creation"></a>Küme oluşturma sırasında uygulama yükleme
Bir küme oluştururken hello seçeneği tooinstall Hdınsight uygulamaları vardır. Merhaba küme oluşturulur ve çalışır durumda hello sonra hello işlemi sırasında Hdınsight uygulamaları yüklenir. Merhaba aşağıdaki yordamda nasıl gösterilmektedir bir küme oluştururken tooinstall Hdınsight uygulamaları.

**tooinstall Hdınsight uygulaması**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. **YENİ** öğesine, **Veri + Analiz** öğesine ve ardından **HDInsight**'a tıklayın.
3. **Küme Adı** girin: Bu ad genel olarak benzersiz olmalıdır.
4. Tıklatın **abonelik** tooselect hello hello kümesi için kullanılan Azure aboneliği.
5. **Küme Türü Seçin**’e tıklayın ve ardından şunu seçin:
   
   * **Küme türü**: hangi toochoose bilmiyorsanız seçin **Hadoop**. Merhaba en popüler küme türü budur.
   * **İşletim Sistemi**: **Linux** seçeneğini belirleyin.
   * **Sürüm**: hangi toochoose bilmiyorsanız hello varsayılan sürümü kullanın. Daha fazla bilgi için bkz. [HDInsight küme sürümleri](hdinsight-component-versioning.md).
   * **Küme katmanı**: Azure Hdınsight iki kategoride hello büyük veri Bulutu teklifleri sunar: standart katmanı ve Premium katmanı. Daha fazla bilgi için bkz. [Küme katmanları](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Tıklatın **uygulamaları**, hello birini yayımlanan uygulamaları ve ardından tıklatın **seçin**.
7. Tıklatın **kimlik bilgileri** ve hello yönetici kullanıcı için bir parola girin. Tooenter etmeniz bir **SSH kullanıcı adı** ve ya da bir **parola** veya **ortak anahtar**, kullanılan tooauthenticate hello SSH kullanıcı olduğu. Ortak anahtar kullanılması önerilen yaklaşımı hello ' dir. Tıklatın **seçin** hello alt toosave hello kimlik bilgileri yapılandırması sırasında.
8. Tıklatın **veri kaynağı**, var olan depolama hesapları hello birini seçin veya hello varsayılan depolama hesabı olarak hello kümesi için kullanılan yeni bir depolama hesabı toobe oluşturun.
9. ' I tıklatın **kaynak grubu** tooselect var olan bir kaynak grubu ya da tıklatın **yeni** toocreate yeni bir kaynak grubu
10. Merhaba üzerinde **yeni Hdınsight kümesi** dikey penceresinde emin **PIN tooStartboard** seçilir ve ardından **oluşturma**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Yüklü HDInsight uygulamalarını ve özelliklerini listeleme
Merhaba portal hello listesini bir küme ve her bir uygulama hello özellikleri için HDInsight uygulamaları yüklü gösterir.

**toolist Hdınsight uygulama ve görüntü özellikleri**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello soldaki menüde.  Bu seçeneği görmüyorsanız **Gözat**’a ve ardından **HDInsight Kümeleri**’ne tıklayın.
3. Bir HDInsight kümesine tıklayın.
4. Merhaba gelen **ayarları** dikey penceresinde tıklatın **uygulamaları** hello altında **genel** kategorisi. Merhaba yüklü uygulamalar dikey penceresinde tüm yüklü hello uygulamaları listeler. 
   
    ![HDInsight uygulamaları yüklü uygulamalar](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Merhaba yüklü uygulamalar tooshow hello özelliği birini tıklatın. Merhaba özellik dikey penceresinde listelenir:
   
   * Uygulama adı: uygulamanın adı.
   * Durum: uygulamanın durumu. 
   * Web sayfası: Merhaba web uygulaması toohello kenar düğümüne dağıttığınız hello URL'si. Merhaba kimlik bilgisi hello HTTP kullanıcı, kimlik bilgileri aynı hello kümesi için yapılandırdığınız hello ' dir.
   * HTTP uç noktası: hello kimlik olduğundan hello aynı hello HTTP kullanıcı, kimlik bilgileri gibi hello küme için yapılandırıldığından. 
   * SSH uç noktası: SSH tooconnect toohello kenar düğümünü kullanabilirsiniz. Merhaba SSH kullanıcı, kimlik bilgileri aynı hello kümesi için yapılandırdığınız hello Hello SSH kimlik bilgileridir. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).
6. bir uygulama, toodelete hello uygulamaya sağ tıklayın ve ardından **silmek** hello bağlam menüsünden.

## <a name="connect-toohello-edge-node"></a>Toohello kenar düğümüne bağlanma
HTTP ve SSH kullanarak toohello kenar düğümüne bağlanabilirsiniz. Merhaba uç nokta bilgileri hello bulunabilir [portal](#list-installed-hdinsight-apps-and-properties). Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

Merhaba HTTP uç noktası kimlik bilgilerini hello Hdınsight kümesi için yapılandırdığınız hello HTTP kullanıcı kimlik bilgileridir; Merhaba SSH uç noktası kimlik bilgilerini hello Hdınsight kümesi için yapılandırdığınız hello SSH kimlik bilgileridir.

## <a name="troubleshoot"></a>Sorun giderme
Bkz: [hello yükleme sorunlarını giderme](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Sonraki adımlar
* [Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): öğrenin nasıl toodeploy yayımlanmamış bir Hdınsight uygulaması tooHDInsight.
* [Hdınsight uygulamalarını yayımlama](hdinsight-apps-publish-applications.md): öğrenin nasıl toopublish, özel Hdınsight uygulamaları tooAzure Market.
* [MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx): öğrenin nasıl toodefine Hdınsight uygulamaları.
* [Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md): öğrenin nasıl toouse betik eylemi tooinstall ek uygulamalar.
* [Resource Manager şablonları kullanarak Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md): nasıl toocall Resource Manager şablonları toocreate Hdınsight kümeleri öğrenin.
* [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md): nasıl toouse boş bir kenar düğümü Hdınsight kümesine erişmek, Hdınsight uygulamalarını test etme ve barındırma öğrenin Hdınsight uygulamaları.

