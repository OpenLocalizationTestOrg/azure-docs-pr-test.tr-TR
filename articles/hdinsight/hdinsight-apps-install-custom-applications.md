---
title: "aaaInstall kendi özel Azure Hdınsight Hadoop uygulamaları | Microsoft Docs"
description: "Bilgi nasıl Hdınsight uygulamalarına Hdınsight uygulamalarını tooinstall."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Azure HDInsight'a özel Hadoop uygulamaları yükleme

Bu makalede, nasıl tooinstall değiştirilmediğinden Azure hdınsight'ta Hadoop uygulama toohello Azure portalında yayımlanmış öğreneceksiniz. Bu makalede yükleyeceğiniz hello uygulama [Hue](http://gethue.com/).

HDInsight uygulaması kullanıcıların Linux tabanlı HDInsight kümesine yükleyebileceği bir uygulamadır.  Bu uygulamalar Microsoft veya bağımsız yazılım satıcıları (ISV) tarafından ya da sizin tarafınızdan geliştirilebilir.  

Diğer ilgili makaleler:

* [Hdınsight uygulamaları yükleme](hdinsight-apps-install-applications.md): tooinstall bir Hdınsight uygulaması tooyour nasıl kümeleri öğrenin.
* [Hdınsight uygulamalarını yayımlama](hdinsight-apps-publish-applications.md): öğrenin nasıl toopublish, özel Hdınsight uygulamaları tooAzure Market.
* [MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx): öğrenin nasıl toodefine Hdınsight uygulamaları.

## <a name="prerequisites"></a>Ön koşullar
Mevcut bir Hdınsight kümesine Hdınsight uygulamalarını tooinstall istiyorsanız bir Hdınsight kümesi olması gerekir. toocreate biri bkz [küme oluşturma](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). HDInsight uygulamalarını ayrıca bir HDInsight kümesi oluştururken yükleyebilirsiniz.

## <a name="install-hdinsight-applications"></a>HDInsight uygulamaları yükleme
Bir küme veya tooan varolan Hdınsight kümesi oluştururken Hdınsight uygulamaları yüklenir. Azure Resource Manager şablonlarını tanımlamak için bkz. [MSDN: HDInsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx).

Bu uygulamayı (Hue) dağıtmak için gerekli hello dosyalar:

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): Hdınsight uygulaması yüklemek için hello Resource Manager şablonu. Kendi Azure Resource Manager şablonunuzu geliştirmek için bkz. [MSDN: HDInsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx).
* [Hue-install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello hello kenar düğümünü yapılandırmak için hello Resource Manager şablonu tarafından çağrılan betik eylemi.
* [Hue-binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hui-install_v0.sh dosyasından çağrılan hello hue ikili dosyası.
* [Hue-ikili-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): hui-install_v0.sh dosyasından çağrılan hello hue ikili dosyası.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): hui-install_v0.sh dosyasından çağrılan bir örnek web uygulaması (Tomcat).

**tooinstall ton tooan varolan Hdınsight kümesi**

1. Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Bu düğme hello Azure portalında bir Resource Manager şablonu açar.  Merhaba Resource Manager şablonu konumundadır [https://github.com/hdinsight/Iaas-Applications/Tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn nasıl toowrite bu Resource Manager şablonunu bkz [MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx).
2. Merhaba gelen **parametreleri** dikey penceresinde hello aşağıdakileri girin:

   * **ClusterName**: tooinstall Merhaba uygulaması istediğiniz hello hello kümenin adını girin. Bu küme var olan bir küme olmalıdır.
3. Tıklatın **Tamam** toosave hello parametreleri.
4. Merhaba gelen **özel dağıtım** dikey penceresinde girin **kaynak grubu**.  Merhaba kaynak grubu hello küme, hello bağımlı depolama hesabı ve diğer kaynakları gruplandıran bir kapsayıcıdır. Gerekli toouse hello hello küme aynı kaynak grubunda.
5. **Yasal koşullar**’a ve ardından **Oluştur**’a tıklayın.
6. Merhaba doğrulayın **PIN toodashboard** onay kutusu seçilidir ve ardından **oluşturma**. Merhaba döşeme sabitlenmiş toohello portal Pano ve hello portal bildirim (Merhaba portal hello üstündeki hello zil simgesine tıklayın) hello yükleme durumunu görebilirsiniz.  Tooinstall Merhaba uygulaması yaklaşık 10 dakika sürer.

**bir küme oluştururken Hue tooinstall**

1. Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Bu düğme hello Azure portalında bir Resource Manager şablonu açar.  Merhaba Resource Manager şablonu konumundadır [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn nasıl toowrite bu Resource Manager şablonunu bkz [MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx).
2. Merhaba yönerge toocreate küme izleyin ve Hue yükleyin. HDInsight kümeleri oluşturma hakkında daha fazla bilgi için bkz. [HDInsight’ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

Ayrıca toohello Azure portal, ayrıca kullanabileceğiniz [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) ve [Azure CLI](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall Resource Manager şablonları.

## <a name="validate-hello-installation"></a>Merhaba yüklemeyi doğrulama
Hello Azure portal toovalidate hello uygulama yüklemesi hello uygulama durumunu denetleyebilirsiniz. Ayrıca, varsa aynı zamanda tüm HTTP uç noktaları beklenen şekilde geldiğini ve hello Web sayfasını doğrulayabilirsiniz:

**tooopen hello Hue portalını**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello soldaki menüde.  Bu seçeneği görmüyorsanız **Gözat**’a ve ardından **HDInsight Kümeleri**’ne tıklayın.
3. Merhaba uygulaması yüklendiği hello kümesine tıklayın.
4. Merhaba gelen **ayarları** dikey penceresinde tıklatın **uygulamaları** hello altında **genel** kategorisi. Göreceksiniz **hue** hello listelenen **yüklü uygulamalar** dikey.
5. Tıklatın **ton** hello listesi toolist hello özelliklerinden.  
6. Merhaba Web sayfası bağlantısı toovalidate hello Web sitesi'ı tıklatın; Merhaba HTTP uç noktası bir tarayıcı toovalidate hello Hue web kullanıcı Arabirimi, açık hello SSH uç noktası SSH kullanarak açın. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Merhaba yükleme sorunlarını giderme
Merhaba portal bildirim hello uygulama yükleme durumunu kontrol edebilirsiniz (Merhaba portalı hello üstte hello zil simgesine tıklayın).

Bir uygulama yüklemesi başarısız olursa hello hata iletilerine bakın ve hata ayıklama bilgileri 3 yerden:

* HDInsight Uygulamaları: genel hata bilgileri.

    Merhaba küme hello portalından açın ve hello ayarları dikey penceresinden Uygulamalar'a tıklayın:

    ![hdinsight applications application installation error](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Hdınsight betik eylemi: Merhaba Hdınsight uygulamalarının hata iletisi bir betik eylemi hatası belirtiyorsa hello komut dosyası hata hakkında daha fazla ayrıntı hello betik eylemleri bölmesinde sunulur.

    Betik eylemi hello ayarlar dikey penceresinden'ı tıklatın. Betik eylemi geçmişi hello hata iletilerini gösterir

    ![hdinsight applications script action error](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web kullanıcı Arabirimi: hello yükleme betiği hello hatanın nedenini hello olduysa, Ambari Web kullanıcı arabirimini toocheck hello yükleme betikleri hakkında tam günlükleri kullanın.

    Daha fazla bilgi için bkz. [Sorun giderme](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>HDInsight uygulamalarını kaldırma
Çeşitli yolları toodelete Hdınsight uygulamaları vardır.

### <a name="use-portal"></a>Portal kullanma
**tooremove hello portal kullanarak uygulama**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **Hdınsight kümeleri** hello soldaki menüde.  Bu seçeneği görmüyorsanız **Gözat**’a ve ardından **HDInsight Kümeleri**’ne tıklayın.
3. Merhaba uygulaması yüklendiği hello kümesine tıklayın.
4. Merhaba gelen **ayarları** dikey penceresinde tıklatın **uygulamaları** hello altında **genel** kategorisi. Yüklü uygulamalar listesini görmeniz gerekir. Bu öğretici için **hue** hello listelenen **yüklü uygulamalar** dikey.
5. Tooremove istediğiniz ve ardından hello uygulamayı sağ **silmek**.
6. Tıklatın **Evet** tooconfirm.

Merhaba Portalı'ndan hello küme silin veya Merhaba uygulaması içeren hello kaynak grubunu silebilirsiniz.

### <a name="use-azure-powershell"></a>Azure PowerShell kullanma
Azure PowerShell kullanarak, hello küme silin veya hello kaynak grubunu silin. Bkz. [Azure PowerShell kullanarak küme silme](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Azure CLI kullanma
Azure CLI kullanarak hello küme silin veya hello kaynak grubunu silin. Bkz. [Azure CLI kullanarak küme silme](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Sonraki adımlar
* [MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx): öğrenin nasıl Hdınsight uygulamalarını dağıtmaya toodevelop Resource Manager şablonları.
* [Hdınsight uygulamaları yükleme](hdinsight-apps-install-applications.md): tooinstall bir Hdınsight uygulaması tooyour nasıl kümeleri öğrenin.
* [Hdınsight uygulamalarını yayımlama](hdinsight-apps-publish-applications.md): öğrenin nasıl toopublish, özel Hdınsight uygulamaları tooAzure Market.
* [Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md): öğrenin nasıl toouse betik eylemi tooinstall ek uygulamalar.
* [Resource Manager şablonları kullanarak Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md): nasıl toocall Resource Manager şablonları toocreate Hdınsight kümeleri öğrenin.
* [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md): nasıl toouse boş bir kenar düğümü Hdınsight kümesine erişmek, Hdınsight uygulamalarını test etme ve barındırma öğrenin Hdınsight uygulamaları.
