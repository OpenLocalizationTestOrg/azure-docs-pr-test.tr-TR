---
title: "aaaUse boş hdınsight'ta - Azure Hadoop kümelerde edge düğüm | Microsoft Docs"
description: "Nasıl tooadd boş kenar düğümü tooan Hdınsight küme, bir istemci olarak kullanılabilir ve ardından test/Hdınsight uygulamalarınızı ana bilgisayarı."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Hdınsight'ta Hadoop kümeleri üzerinde boş kenar düğümleri kullanın

Nasıl tooadd boş bir kenar düğümü tooan Hdınsight kümesi hakkında bilgi edinin. Linux sanal makine ile aynı istemci araçları yüklü ve yapılandırılmış olduğu gibi hello headnodes hello ancak çalışan hiçbir Hadoop Hizmetleri bir boş kenar düğümdür. Merhaba kenar düğümüne hello küme erişmek, istemci uygulamalarınızı test etme ve istemci uygulamalarını barındırmak için kullanabilirsiniz. 

Merhaba Küme oluşturduğunuzda bir boş kenar düğümü tooan varolan Hdınsight kümesi, yeni küme tooa ekleyebilirsiniz. Bir boş kenar düğümüne ekleyerek yapılır Azure Resource Manager şablonu kullanarak.  Merhaba aşağıdaki örnek nasıl yapıldığını gösteren bir şablon kullanarak:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Merhaba örnekte gösterildiği gibi isteğe bağlı olarak çağırabilirsiniz bir [betik eylemi](hdinsight-hadoop-customize-cluster-linux.md) yükleme gibi ek yapılandırma tooperform, [Apache ton](hdinsight-hadoop-hue-linux.md) hello kenar düğümünde. Merhaba betik eylemi betik hello Web'de genel olarak erişilebilir olmalıdır.  Merhaba komut dosyası Azure depolama alanında depolanır, örneğin, genel kapsayıcılar veya genel BLOB'lar kullanın.

Merhaba kenar düğümü sanal makine boyutu hello Hdınsight küme çalışan düğümü vm boyutu gereksinimlerini karşılaması gerekir. Merhaba çalışan düğümü vm boyutları önerilen için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Bir edge düğümünü oluşturduktan sonra SSH kullanarak toohello kenar düğümüne bağlanmak ve istemci araçları tooaccess hello Hadoop kümesi Hdınsight'ta çalıştırın.

> [!WARNING] 
> Hdınsight ile boş kenar düğümünü kullanarak şu anda önizlemede değil. Merhaba kenar düğümüne yüklenir özel bileşenler Microsoft ticari koşulların elverdiği oranda makul desteği alabilirsiniz. Bu, karşılaştığınız sorunları çözme konusunda neden olabilir. Veya daha fazla yardım için başvurulan toocommunity kaynakları olabilir. Merhaba alma çoğu etkin siteler hello topluluktan Yardım hello bazıları şunlardır:
>
> * [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://StackOverflow.com](http://stackoverflow.com).
>
> Apache teknolojisi kullanıyorsanız, Apache proje sitelerinde hello mümkün toofind yardımla olabilir [http://apache.org](http://apache.org), hello gibi [Hadoop](http://hadoop.apache.org/) site.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Edge düğüm tooan varolan bir kümeye ekleme
Bu bölümde, Resource Manager şablonu tooadd kenar düğümü tooan varolan Hdınsight kümesi kullanın.  Merhaba Resource Manager şablonu bulunabilir [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). Merhaba Resource Manager şablonu https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh bulunan bir betik eylemi çağırır. Merhaba betik eylemleri gerçekleştirmez.  Resource Manager şablonu betik eylemi çağırma toodemonstrate olur.

**tooadd boş kenar düğümü tooan varolan bir kümeye**

1. Henüz yoksa, Hdınsight kümesi oluşturun.  Bkz: [Hadoop Öğreticisi: Hdınsight'ta Hadoop kullanmaya başlamanıza](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Görüntü toosign tooAzure olarak ve açık hello Azure Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Aşağıdaki özelliklere hello yapılandırın:
   
   * **Abonelik**: hello küme oluşturmak için kullanılan Azure aboneliğini seçin.
   * **Kaynak grubu**: hello varolan Hdınsight kümesi için kullanılan Select hello kaynak grubu.
   * **Konum**: hello olan bir Hdınsight kümesine hello konumunu seçin.
   * **Küme adı**: mevcut bir Hdınsight kümesine hello adını girin.
   * **Kenar düğüm boyutu**: hello VM boyutları birini seçin. Merhaba vm boyutu hello çalışan düğümü vm boyutu gereksinimlerini karşılaması gerekir. Merhaba çalışan düğümü vm boyutları önerilen için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Kenar düğümü önek**: hello varsayılan değer **yeni**.  Merhaba varsayılan değer, hello edge düğüm adı kullanmaktır **edgenode yeni**.  Merhaba portal hello önekten özelleştirebilirsiniz. Merhaba şablondan hello tam adını da özelleştirebilirsiniz.

4. Denetleme **toohello hüküm ve koşullar yukarıda belirtildiği kabul**ve ardından **satın alma** toocreate hello kenar düğümüne.

>[!IMPORTANT]
> Merhaba varolan Hdınsight kümesi için emin tooselect hello Azure kaynak grubu olun.  Aksi takdirde, ileti "iç içe kaynak üzerinde istenen işlem gerçekleştirilemiyor. hello hata Al Üst kaynak '&lt;ClusterName >' bulunamadı. "

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Bir küme oluştururken bir kenar düğümüne ekleyin
Bu bölümde, bir Resource Manager şablonu toocreate Hdınsight kümesi ile bir edge düğümünü kullanın.  Merhaba Resource Manager şablonu hello bulunabilir [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). Merhaba Resource Manager şablonu https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh bulunan bir betik eylemi çağırır. Merhaba betik eylemleri gerçekleştirmez.  Resource Manager şablonu betik eylemi çağırma toodemonstrate olur.

**tooadd boş kenar düğümü tooan varolan bir kümeye**

1. Henüz yoksa, Hdınsight kümesi oluşturun.  Bkz: [Hdınsight'ta Hadoop kullanmaya başlamanıza](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Görüntü toosign tooAzure olarak ve açık hello Azure Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Aşağıdaki özelliklere hello yapılandırın:
   
   * **Abonelik**: hello küme oluşturmak için kullanılan Azure aboneliğini seçin.
   * **Kaynak grubu**: hello kümesi için kullanılan yeni bir kaynak grubu oluşturun.
   * **Konum**: hello kaynak grubu için bir konum seçin.
   * **Küme adı**: hello yeni küme toocreate için bir ad girin.
   * **Oturum açma kullanıcı adı küme**: Merhaba Hadoop HTTP kullanıcı adı girin.  Merhaba varsayılan ad **yönetici**.
   * **Oturum açma parolası küme**: Merhaba Hadoop HTTP kullanıcı parolasını girin.
   * **SSH kullanıcı adı**: hello SSH kullanıcı adı girin. Merhaba varsayılan ad **sshuser**.
   * **SSH parolası**: hello SSH kullanıcı parolasını girin.
   * **Yükleme komut dosyası eylemi**: Bu öğreticide gitmek için varsayılan değer hello tutun.
     
     Bazı özellikler sabit kodlanmış hello şablonunda olmuştur: küme türü, küme çalışan düğüm sayısı, Edge düğüm boyutu ve kenar düğüm adı.
4. Denetleyin **toohello hüküm ve koşullar yukarıda belirtildiği kabul**ve ardından **satın alma** toocreate hello küme hello kenar düğümüne sahip.

## <a name="access-an-edge-node"></a>Bir kenar düğümüne erişin
Merhaba kenar düğümüne ssh uç noktadır &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.  Örneğin, yeni-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

Merhaba kenar düğümüne hello Azure portalında bir uygulama olarak görünür.  bilgi tooaccess hello hello hello portal verir düğümü SSH kullanarak kenar.

**tooverify hello kenar düğümü SSH uç noktası**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hdınsight kümesi ile bir edge düğümünü açın.
3. Tıklatın **uygulamaları** hello küme dikey penceresinden. Merhaba kenar düğümünü göreceksiniz.  Merhaba varsayılan ad **edgenode yeni**.
4. Merhaba kenar düğümüne tıklayın. Merhaba SSH uç noktası göreceksiniz.

**toouse hello kenar düğümüne yığını**

1. SSH tooconnect toohello kenar düğümünü kullanın. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH kullanarak kenar düğümüne toohello bağlandıktan sonra komut tooopen hello Hive konsolundan aşağıdaki hello kullan:
   
        hive
3. Komut tooshow Hive tablolarını hello kümedeki aşağıdaki hello çalıştırın:
   
        show tables;

## <a name="delete-an-edge-node"></a>Bir kenar düğümüne Sil
Azure portal hello bir kenar düğümüne silebilirsiniz.

**tooaccess bir kenar düğümüne**

1. Toohello üzerinde oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hdınsight kümesi ile bir edge düğümünü açın.
3. Tıklatın **uygulamaları** hello küme dikey penceresinden. Edge düğüm listesi göreceksiniz.  
4. Toodelete istediğiniz ve ardından sağ hello kenar düğümüne **silmek**.
5. Tıklatın **Evet** tooconfirm.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrendiğiniz nasıl tooadd bir edge düğümünü ve nasıl tooaccess kenar düğümüne hello. toolearn daha makaleler hello bakın:

* [Hdınsight uygulamaları yükleme](hdinsight-apps-install-applications.md): tooinstall bir Hdınsight uygulaması tooyour nasıl kümeleri öğrenin.
* [Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): öğrenin nasıl toodeploy yayımlanmamış bir Hdınsight uygulaması tooHDInsight.
* [Hdınsight uygulamalarını yayımlama](hdinsight-apps-publish-applications.md): öğrenin nasıl toopublish, özel Hdınsight uygulamaları tooAzure Market.
* [MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx): öğrenin nasıl toodefine Hdınsight uygulamaları.
* [Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md): öğrenin nasıl toouse betik eylemi tooinstall ek uygulamalar.
* [Resource Manager şablonları kullanarak Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md): nasıl toocall Resource Manager şablonları toocreate Hdınsight kümeleri öğrenin.

