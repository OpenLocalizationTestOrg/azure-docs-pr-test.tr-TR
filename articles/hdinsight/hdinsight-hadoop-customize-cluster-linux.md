---
title: "Betik eylemleri - Azure kullanarak Hdınsight kümelerini özelleştirme | Microsoft Docs"
description: "Özel bileşenler için betik eylemleri kullanarak Linux tabanlı Hdınsight kümelerini ekleyin. Betik eylemleri küme yapılandırmasını özelleştirebilir veya ek hizmetleri ve yardımcı programları ton, Solr veya r gibi eklemek için kullanılan Bash betikleridir"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme

Hdınsight adlı bir yapılandırma seçeneği sağlar **betik eylemi** küme özelleştirme özel komut dosyaları çağırır. Bu komut dosyalarını ek bileşenler yükleme ve yapılandırma ayarlarını değiştirmek için kullanılır. Betik eylemleri, sırasında veya Küme oluşturulduktan sonra kullanılabilir.

> [!IMPORTANT]
> Betik eylemleri zaten çalışan bir kümede kullanma olanağı yalnızca Linux tabanlı Hdınsight kümeleri için kullanılabilir.
>
> Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Betik eylemleri de Azure Marketi'nde bir Hdınsight uygulaması olarak yayımlanabilir. Bu belgedeki örneklerde bazıları, PowerShell ve .NET SDK'sı betik eylemi komutları kullanarak bir Hdınsight uygulamasının nasıl yükleyebileceğinizi gösterir. Hdınsight uygulamaları hakkında daha fazla bilgi için bkz: [yayımlama Hdınsight uygulamalarını Azure Marketi'nde](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>İzinler

Bir etki alanına katılmış Hdınsight kümesi kullanıyorsanız, betik eylemleri kümeyle kullanırken gerekli olan iki Ambari izinleri vardır:

* **AMBARI. ÇALIŞTIRMA\_özel\_KOMUTU**: Ambari Yönetici rolü varsayılan olarak bu izne sahiptir.
* **KÜME. ÇALIŞTIRMA\_özel\_KOMUTU**: her iki Hdınsight küme yöneticisinin ve Ambari yönetici varsayılan olarak bu izne sahip.

İzinleri etki alanına katılmış Hdınsight ile çalışma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Erişim denetimi

Hesabınızın, Azure aboneliğinizin Yöneticisi/sahibi değilseniz, en az olmalı **katkıda bulunan** Hdınsight kümesi içeren kaynak grubuna erişim.

Ayrıca, Hdınsight kümesi, birisi ile en az oluşturuyorsanız **katkıda bulunan** Azure aboneliğine erişiminiz gerekir daha önce kaydettiğiniz Hdınsight için sağlayıcı. Sağlayıcı kaydı, aboneliğe Katkıda Bulunan erişimi olan bir kullanıcı abonelikte ilk kez kaynak oluşturduğunda gerçekleşir. Bu işlem ayrıca [REST ile bir sağlayıcı kaydedilerek](https://msdn.microsoft.com/library/azure/dn790548.aspx) kaynak oluşturulmadan gerçekleştirilebilir.

Erişim yönetimiyle çalışma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:

* [Azure portalında erişim yönetimi ile çalışmaya başlama](../active-directory/role-based-access-control-what-is.md)
* [Azure abonelik kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Anlama betik eylemleri

Bir komut dosyası yalnızca bir URI sağlayın Bash komut dosyası ve parametreleri bir eylemdir. Hdınsight küme düğümlerinde komut dosyasını çalıştırır. Aşağıdaki özellikleri ve betik eylemleri özelliklerini geçerlidir.

* Hdınsight küme erişilebilen bir URI üzerinde depolanmalıdır. Olası depolama konumları şunlardır:

    * Bir **Azure Data Lake Store** Hdınsight küme tarafından erişilebilir olan hesap. Hdınsight ile Azure Data Lake Store hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Data Lake Store'da depolanan bir komut dosyası kullanıldığında, URI biçimi `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Hdınsight Data Lake Store erişmek için kullandığı hizmet sorumlusu komut dosyasını okuma erişimi olması gerekir.

    * Bir blobu bir **Azure depolama hesabı** diğer bir deyişle ya da birincil ya da ek depolama hesabı için Hdınsight kümesi. Hdınsight küme oluşturma sırasında iki depolama hesapları bu tür erişim verilir.

    * Paylaşım Hizmeti Azure Blob, GitHub, OneDrive, Dropbox, vb. gibi ortak bir dosya.

        URI, örneğin bkz [örnek betik eylemi betikler](#example-script-action-scripts) bölümü.

        > [!WARNING]
        > Hdınsight yalnızca destekler __genel amaçlı__ Azure depolama hesapları. Şu anda desteklemediği __Blob storage__ hesap türü.

* Kısıtlanmış olabilir **yalnızca belirli düğüm türleri üzerinde çalıştırmak**örnek baş düğümler ve çalışan düğümleri için.

  > [!NOTE]
  > Hdınsight Premium ile birlikte kullanıldığında, komut dosyası edge düğüm üzerinde kullanılmalıdır belirtebilirsiniz.

* Olabilir **kalıcı** veya **geçici**.

    **Kalıcı** komut dosyaları, komut çalıştıktan sonra kümesine çalışan düğümlerine uygulanır. Örneğin, küme ölçeklendirme.

    Kalıcı bir betik, ayrıca bir baş düğüm gibi başka bir düğüm türü için değişiklikler uygulanabilir.

  > [!IMPORTANT]
  > Kalıcı betik eylemleri benzersiz bir ad olmalıdır.

    **Geçici** betikleri kalıcı değildir. Çalışan düğümlerine sahip komut dosyasını çalıştırdıktan sonra kümesine uygulanmaz. Daha sonra kalıcı bir betik için geçici bir komut dosyası yükseltmek veya geçici bir komut dosyası için kalıcı bir betik indirgemek.

  > [!IMPORTANT]
  > Küme oluşturma sırasında kullanılan betik eylemleri otomatik olarak kalıcıdır.
  >
  > Başarısız olmayan betikleri özellikle olması gerektiğini belirtmek olsa bile kalıcı.

* Kabul edebilir **parametreleri** kullanılan komut dosyası tarafından yürütme sırasında.
* Çalıştırma **kök düzeyinde ayrıcalıklara** küme düğümlerinde.
* Aracılığıyla kullanılan **Azure portal**, **Azure PowerShell**, **Azure CLI**, veya **Hdınsight .NET SDK'sı**

Küme çalıştırdığınız sahip tüm betikler geçmişini tutar. Geçmiş, yükseltme veya indirgeme işlemleri için bir komut dosyası Kimliğini bulmanız gerektiğinde kullanışlıdır.

> [!IMPORTANT]
> Bir komut dosyası eylemi tarafından yapılan değişiklikleri geri almak için otomatik bir yolu yoktur. El ile değişikliklerinizi geri ya da bunları tersine çevirir bir komut dosyası sağlar.


### <a name="script-action-in-the-cluster-creation-process"></a>Küme oluşturma işlemi betik eylemi

Küme oluşturma sırasında kullanılan betik eylemleri eylemler var olan bir küme üzerinde çalışan komut dosyasından biraz farklılık gösterir:

* Komut dosyası **otomatik olarak kalıcı**.
* A **hatası** komut dosyasında küme oluşturma işleminin başarısız olmasına neden olabilir.

Betik eylemi oluşturma işlemi sırasında çalıştırıldığında aşağıdaki diyagramda gösterilmektedir:

![Hdınsight küme özelleştirme ve küme oluşturma sırasında aşamaları][img-hdi-cluster-states]

Hdınsight yapılandırılırken komut dosyasını çalıştırır. Bu aşamada, betik belirtilen kümedeki tüm düğümler üzerinde paralel olarak çalışır ve düğümlerde kök ayrıcalıklarıyla çalıştırır.

> [!NOTE]
> Komut dosyası kök düzeyinde ayrıcalığıyla küme düğümleri üzerinde çalıştığı için durdurma ve Hadoop ile ilgili hizmetlerin gibi hizmetler başlatma gibi işlemler gerçekleştirebilirsiniz. Hizmetleri durdurun, çalışan betik tamamlanmadan önce Ambari hizmet ve diğer Hadoop ile ilgili hizmetlerin hazır ve çalışır olduğundan emin olmalısınız. Bu hizmetler, oluşturulurken başarıyla sistem durumunu ve küme durumunu belirlemek için gereklidir.


Küme oluşturma sırasında aynı anda birden çok betik eylemleri kullanabilirsiniz. Bu komut belirtilen sırada çağrılır.

> [!IMPORTANT]
> Betik eylemleri, 60 dakika veya zaman aşımı içinde tamamlamanız gerekir. Küme hazırlama sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak komut dosyasını çalıştırır. CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden tamamlanması daha uzun sürmesine betik neden olabilir.
>
> Komut dosyasını çalıştırmak için gereken süreyi en aza indirmek için karşıdan yükleme ve kaynak uygulamalardan derleme gibi görevleri kaçının. Uygulamaları önceden derleme ve Azure depolama alanına ikili depolar.


### <a name="script-action-on-a-running-cluster"></a>Betik eylemi çalıştıran bir kümede

Aksine, bir komut dosyasında hata küme oluşturma sırasında kullanılan eylemler zaten çalışan bir küme üzerinde çalışan komut dosyası otomatik olarak başarısız duruma değiştirmek küme neden olmaz. Bir komut dosyası tamamlandıktan sonra kümenin bir "çalışır" duruma dönmesi gerekir.

> [!IMPORTANT]
> Küme bir 'çalışıyor' durumuna sahip olsa bile, başarısız olan kodu şeyler kopuk olabilir. Örneğin, bir komut dosyası küme için gerekli dosyaları silebilir.
>
> Kümenize uygulamadan önce bir komut dosyası yaptığı anladığınızdan emin olmanız gerekir böylece komut dosyalarını eylemleri kök ayrıcalıkları ile çalıştırın.

Bir komut dosyası bir kümeye uygularken, küme durumunu için değişiklikleri **çalıştıran** için **kabul edilen**, ardından **Hdınsight yapılandırma**ve son olarak yeniden **çalıştıran** başarılı bir komut dosyası. Komut durumu betik eylemi geçmişinde kaydedilir ve komut başarılı veya başarısız olup olmadığını belirlemek için bu bilgileri kullanın. Örneğin, `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet, bir komut dosyası durumunu görüntülemek için kullanılabilir. Bilgi aşağıdaki metni benzer döndürür:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Küme oluşturulduktan sonra küme kullanıcı (Yönetici) parolasını değiştirdiyseniz, bu küme karşı eylemler çalışan betik başarısız olabilir. Bu hedef çalışan düğümleri kalıcı betik eylemleri varsa, küme ölçeklendirdiğinizde bu komut dosyaları başarısız olabilir.

## <a name="example-script-action-scripts"></a>Örnek betik eylemi betikler

Betik eylemi komut dosyaları aşağıdaki yardımcı programlar kullanılabilir:

* Azure portalına
* Azure PowerShell
* Azure CLI
* HDInsight .NET SDK'sı

Hdınsight Hdınsight kümelerinde aşağıdaki bileşenleri yüklemek için komut dosyaları sağlar:

| Ad | Betik |
| --- | --- |
| **Bir Azure depolama hesabı ekleme** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.sh. Bkz: [Hdınsight kümesi için ek depolama alanı eklentisi](hdinsight-hadoop-add-storage.md). |
| **Hue yüklemek** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/install-Hue-uber-v02.sh. Bkz: [yükleme ve kullanma ton hdınsight kümeleri](hdinsight-hadoop-hue-linux.md). |
| **Presto yükleyin** |https://RAW.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Bkz: [yükleme ve kullanma Presto hdınsight kümeleri](hdinsight-hadoop-install-presto.md). |
| **Solr yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-installer-v01.sh. Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install-linux.md). |
| **Giraph yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install-linux.md). |
| **Ön yük Hıve kitaplıkları** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Bkz: [eklemek Hive kitaplıkları Hdınsight kümelerinde](hdinsight-hadoop-add-hive-libraries.md). |
| **Mono yükleme veya güncelleştirme** | https://hdiconfigactions.BLOB.Core.Windows.NET/install-Mono/install-Mono.bash. Bkz: [yükleme veya güncelleştirme Mono hdınsight'ta](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Küme oluşturma sırasında bir betik eylemi kullanın

Bu bölümde, betik eylemleri bir Hdınsight kümesi oluştururken kullanabileceğiniz farklı yolları hakkında örnekler verilmektedir.

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a>Azure portalından küme oluşturma sırasında bir betik eylemi kullanın

1. Konusunda açıklandığı gibi bir küme oluşturmaya başlamak [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md). Ulaştığınızda Durdur __küme Özet__ bölümü.

2. Gelen __küme Özet__ bölümünde, select __Düzenle__ için bağlantı __Gelişmiş ayarları__.

    ![Gelişmiş ayarlar bağlantısı](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Gelen __Gelişmiş ayarları__ bölümünde, select __betik eylemleri__. Gelen __betik eylemleri__ bölümünde, select __+ yeni Gönder__

    ![Yeni betik eylemi Gönder](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Kullanım __bir komut dosyası seçin__ girişi önceden yapılmış bir komut dosyası seçin. Özel bir komut dosyası kullanmayı seçin __özel__ ve ardından sağlayın __adı__ ve __betik URI Bash__ betiği için.

    ![Select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Aşağıdaki tabloda formda öğeleri açıklar:

    | Özellik | Değer |
    | --- | --- |
    | Bir komut dosyası seçin | Kendi komut dosyası kullanmayı seçin __özel__. Aksi durumda, sağlanan komut dosyalarından birini seçin. |
    | Ad |Betik eylemi için bir ad belirtin. |
    | Bash betik URI |Küme özelleştirmek için çağrılan betik URI'si belirtin. |
    | HEAD/çalışan/Zookeeper |Düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) özelleştirme betik çalıştığı şirket. |
    | Parametreler |Komut dosyası tarafından gerekli parametreleri belirtin. |

    Kullanım __bu betik eylemini Sürdür__ komut dosyası işlemleri ölçeklendirme sırasında uygulandığından emin olmak için giriş.

5. Seçin __oluşturma__ komut dosyasını kaydetmek için. Daha sonra __+ gönderme yeni__ başka bir komut dosyası eklemek için.

    ![Birden çok betik eylemleri](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Komut dosyaları eklemeyi bitirdiğinizde, kullanmak __seçin__ düğmesine ve ardından __sonraki__ geri dönmek için düğmesini __küme özeti__ bölümü.

3. Küme oluşturmak için seçin __oluşturma__ gelen __küme Özet__ seçim.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Azure Resource Manager şablonları bir betik eylemi kullanın

Bu bölümdeki örnek betik eylemleri Azure Resource Manager şablonları ile kullanmak nasıl ekleyebileceğiniz gösterilmektedir.

#### <a name="before-you-begin"></a>Başlamadan önce

* Hdınsight Powershell cmdlet'lerini çalıştırmak için bir iş istasyonu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).
* Şablonlarının nasıl oluşturulacağı hakkında yönergeler için bkz [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).
* Resource Manager ile daha önce Azure PowerShell kullanmadıysanız, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Betik eylemi kullanarak kümeleri oluşturma

1. Aşağıdaki şablonu bilgisayarınızdaki bir konuma kopyalayın. Bu şablon Giraph headnodes ve çalışan düğümleri yükler. Ayrıca, JSON şablonunu geçerli olup olmadığını doğrulayabilirsiniz. Şablonunuzu içerik içine yapıştırma [JSONLint](http://jsonlint.com/), bir çevrimiçi JSON doğrulama aracı.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Azure PowerShell ve oturum açma Azure hesabınızda başlatın. Kimlik bilgilerinizi girdikten sonra komutu, hesabınız hakkında bilgiler döndürür.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Birden çok aboneliğiniz varsa, dağıtım için kullanmak istediğiniz abonelik kimliği sağlayın.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Kullanabileceğiniz `Get-AzureRmSubscription` her biri için abonelik Kimliğini içeren, hesabınızla ilişkili tüm Aboneliklerin listesini almak için.

4. Varolan bir kaynak grubu yoksa, bir kaynak grubu oluşturun. Çözümünüz için gereksinim duyduğunuz konumu ve kaynak grubu adını sağlayın. Yeni kaynak grubu özetini döndürülür.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. Kaynak grubunuz için bir dağıtım oluşturmak için çalıştırın **New-AzureRmResourceGroupDeployment** komut ve gerekli parametreleri belirtin. Parametreler aşağıdaki veriler şunları içerir:

    * Dağıtımınız için bir ad
    * Kaynak grubu adı
    * Yolu veya URL'si, oluşturduğunuz şablon.

  Şablonunuzu herhangi bir parametre gerektiriyorsa, bu parametreler de geçmesi gerekir. Bu durumda, küme üzerinde R yüklemek için betik eylemi herhangi bir parametre gerektirmez.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Şablonda tanımlanan parametreler için değerler sağlamanız istenir.

1. Kaynak grubu dağıttığınızda dağıtımın bir özeti gösterilir.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Dağıtımınızı başarısız olursa hatalar hakkında bilgi almak için aşağıdaki cmdlet'leri kullanabilirsiniz.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Azure PowerShell üzerinden küme oluşturma sırasında bir betik eylemi kullanın

Bu bölümde, kullanırız [Ekle AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) bir küme özelleştirmek için betik eylemi kullanarak komut dosyalarını çağrılacak cmdlet'i. Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun. Hdınsight PowerShell cmdlet'lerini çalıştırmak için bir iş istasyonu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).

Aşağıdaki komut dosyası, PowerShell kullanarak bir küme oluştururken, bir komut dosyası eylemi uygulanacak gösterilmiştir:

[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Küme oluşturulmadan önce birkaç dakika sürebilir.

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a>Hdınsight .NET SDK küme oluşturma sırasında bir betik eylemi kullanın

Hdınsight .NET SDK'sı bir .NET uygulamasından Hdınsight ile çalışmayı kolaylaştırır istemci kitaplıkları sağlar. Kod örneği için bkz: [.NET SDK kullanarak Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-to-a-running-cluster"></a>Betik eylemi çalıştıran bir kümeye uygulama

Bu bölümde, betik eylemleri çalıştıran bir kümeye uygulamayı öğrenin.

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a>Betik eylemi çalıştıran bir kümeye Azure portalından uygulayın.

1. Gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.

2. Hdınsight küme genel bakış'tan, seçin **betik eylemleri** döşeme.

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** ayarları bölümünden.

3. Betik eylemleri bölümünde üstten seçin **gönderme yeni**.

    ![Bir komut dosyası çalıştıran bir kümeye ekleme](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Kullanım __bir komut dosyası seçin__ girişi önceden yapılmış bir komut dosyası seçin. Özel bir komut dosyası kullanmayı seçin __özel__ ve ardından sağlayın __adı__ ve __betik URI Bash__ betiği için.

    ![Select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Aşağıdaki tabloda formda öğeleri açıklar:

    | Özellik | Değer |
    | --- | --- |
    | Bir komut dosyası seçin | Kendi komut dosyası kullanmayı seçin __özel__. Aksi durumda, sağlanan komut dosyasını seçin. |
    | Ad |Betik eylemi için bir ad belirtin. |
    | Bash betik URI |Küme özelleştirmek için çağrılan betik URI'si belirtin. |
    | HEAD/çalışan/Zookeeper |Düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) özelleştirme betik çalıştığı şirket. |
    | Parametreler |Komut dosyası tarafından gerekli parametreleri belirtin. |

    Kullanım __bu betik eylemini Sürdür__ komut dosyası işlemleri ölçeklendirme sırasında uygulanan emin olmak için giriş.

5. Son olarak, **oluşturma** betik kümeye uygulamak için düğmesi.

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a>Betik eylemi çalıştıran bir kümeye Azure Powershell'den uygulayın.

Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun. Hdınsight PowerShell cmdlet'lerini çalıştırmak için bir iş istasyonu yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).

Aşağıdaki örnek betik eylemi çalıştıran bir kümeye uygulama gösterilmiştir:

[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

İşlem tamamlandığında, aşağıdakine benzer bilgiler alırsınız:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a>Betik eylemi çalıştıran bir kümeye Azure CLI üzerinden uygulayın.

Devam etmeden önce Azure CLI yükleyip yapılandırdığınızdan emin olun. Daha fazla bilgi için bkz: [Azure CLI yükleme](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. Azure Resource Manager moduna geçmek için komut satırında aşağıdaki komutu kullanın:

        azure config mode arm

2. Azure aboneliğinize kimliğini doğrulamak için aşağıdakileri kullanın.

        azure login

3. Betik eylemi çalıştıran bir kümeye uygulamak için aşağıdaki komutu kullanın

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Bu komutun parametresini atlarsanız, bunlar için istenir. Komut dosyası ile belirtirseniz, `-u` parametreleri kabul belirtebilmeniz için kullanarak `-p` parametresi.

    Geçerli düğüm türleri `headnode`, `workernode`, ve `zookeeper`. Komut dosyası birden çok düğüm türleri için uygulanması gereken, ayrılmış türlerini belirtin. bir ';'. Örneğin, `-n headnode;workernode`.

    Komut dosyası kalıcı hale getirmek için ekleme `--persistOnSuccess`. Ayrıca komut dosyası daha sonra kullanarak kalıcı `azure hdinsight script-action persisted set`.

    İş tamamlandığında, aşağıdakine benzer bir çıktı alırsınız:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a>REST API kullanarak çalışan bir küme için bir betik eylemi Uygula

Bkz: [çalıştırmak betik eylemleri çalıştıran bir kümede](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a>Betik eylemi çalıştıran bir kümeye Hdınsight .NET SDK uygulayın.

Bir kümeye betikleri uygulamak için .NET SDK kullanarak bir örnek için bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Betik eylemleri indirgemek geçmişini görüntülemek ve Yükselt

### <a name="using-the-azure-portal"></a>Azure portalını kullanma

1. Gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.

2. Hdınsight küme genel bakış'tan, seçin **betik eylemleri** döşeme.

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** ayarları bölümünden.

4. Bu küme için komut geçmişini betik eylemleri bölümünde görüntülenir. Bu bilgiler kalıcı komut listesini içerir. Aşağıdaki ekran görüntüsünde, betiği bırakıldı Solr bu küme üzerinde çalışan görebilirsiniz. Ekran kalıcı herhangi bir komut dosyası göstermez.

    ![Betik eylemleri bölümünde](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Bir komut dosyası geçmişinden seçerek bu komut dosyası için özellikler bölümü görüntüler. Ekranın üst kısmından komut dosyasını yeniden çalıştırın ya da bunu yükseltin.

    ![Betik eylemleri özellikleri](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Aynı zamanda **...**  eylemleri gerçekleştirmek için betik eylemleri bölümünde girişleri sağındaki.

    ![Eylemler... komut dosyası kullanımı](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Azure PowerShell’i kullanma

| Aşağıdaki kullan... | Hedef... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Kalıcı betik eylemleri hakkında bilgi alma |
| Get-AzureRmHDInsightScriptActionHistory |Betik eylemleri küme veya belirli bir komut dosyası ayrıntılarını uygulanan geçmişini alma |
| Set-AzureRmHDInsightPersistedScriptAction |Bir geçici betik eylemi kalıcı betik eylemi yükseltir |
| Remove-AzureRmHDInsightPersistedScriptAction |Geçici bir eyleme kalıcı betik eylemi indirger |

> [!IMPORTANT]
> Kullanarak `Remove-AzureRmHDInsightPersistedScriptAction` bir komut dosyası tarafından gerçekleştirilen eylemler geri almaz. Bu cmdlet, yalnızca kalıcı bayrağını kaldırır.

Aşağıdaki örnek betik yükseltin, sonra bir komut dosyası indirgemek için cmdlet'leri kullanmayı gösterir.

[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-the-azure-cli"></a>Azure CLI kullanma

| Aşağıdaki kullan... | Hedef... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Kalıcı betik eylemlerin bir listesini alma |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Belirli kalıcı betik eylemi hakkında bilgi alma |
| `azure hdinsight script-action history list <clustername>` |Betik eylemleri kümeye uygulanan geçmişini alma |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Bir özel betik eylemi hakkında bilgi alma |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Bir geçici betik eylemi kalıcı betik eylemi yükseltir |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Geçici bir eyleme kalıcı betik eylemi indirger |

> [!IMPORTANT]
> Kullanarak `azure hdinsight script-action persisted delete` bir komut dosyası tarafından gerçekleştirilen eylemler geri almaz. Bu cmdlet, yalnızca kalıcı bayrağını kaldırır.

### <a name="using-the-hdinsight-net-sdk"></a>Hdınsight .NET SDK kullanarak

Bir kümeden betik geçmişi almak için .NET SDK kullanarak bir örnek için yükseltmek veya betikleri indirgemek, bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Bu örnek ayrıca .NET SDK kullanarak bir Hdınsight uygulamasının nasıl yükleneceğini gösterir.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Hdınsight kümelerinde kullanılan açık kaynaklı yazılım desteği

Microsoft Azure Hdınsight hizmeti, açık kaynaklı teknolojileri Hadoop biçimlendirilmiş bir ekosistemi kullanır. Microsoft Azure, açık kaynaklı teknolojileri için genel düzeyde desteği sağlar. Daha fazla bilgi için bkz: **destek kapsamı** bölümünü [Azure destek SSS Web sitesine](https://azure.microsoft.com/support/faq/). Hdınsight hizmeti yerleşik bileşenleri için destek, ek bir düzeyi sağlar.

Hdınsight hizmetinde bulunan açık kaynak bileşenleri iki tür vardır:

* **Yerleşik bileşenlerini** -bu bileşenlerin Hdınsight kümelerinde önceden yüklü olduğundan ve küme çekirdek işlevselliğini sağlar. Örneğin, YARN ResourceManager, Hive sorgu dili (HiveQL) ve Mahout kitaplık bu kategoriye ait. Küme bileşenlerin tam bir listesi kullanılabilir [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).
* **Özel bileşenler** -, bir kullanıcı kümesi olarak yükleyebilir veya topluluk bulunan ya da sizin tarafınızdan oluşturulan herhangi bir bileşenin, iş yükü kullanın.

> [!WARNING]
> Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenmektedir. Microsoft Support yalıtmak ve bu bileşenleri ilgili sorunları gidermek için yardımcı olur.
>
> Özel bileşenler, daha fazla sorun gidermenize yardımcı olması için ticari koşulların elverdiği oranda makul destek alırsınız. Microsoft destek sorunu çözmek mümkün olabilir veya bu teknoloji derin uzmanlık bulunduğu açık kaynak teknolojileri için kullanılabilir kanalları gerçekleştirmesine olanak isteyebilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).

Hdınsight hizmeti özel bileşenleri kullanmak için çeşitli yöntemler sunar. Aynı düzeyde desteği nasıl bir bileşen kullanılan veya kümeye yüklü bağımsız olarak uygulanır. En sık karşılaşılan aşağıdaki listede açıklanmaktadır özel bileşenler Hdınsight kümelerinde kullanılabileceği yol vardır:

1. İş gönderme - Hadoop veya diğer tür execute veya özel bileşenleri kullanan işi kümeye gönderilebilir.

2. Küme özelleştirme - küme oluşturma sırasında ek ayarlar ve küme düğümlerinde yüklü özel bileşenleri belirtebilirsiniz.

3. Örnekler - popüler özel bileşenleri, Microsoft ve diğerleri için bu bileşenlerin Hdınsight kümelerinde nasıl kullanılabileceğini örnek sağlayabilir. Bu örnekler desteği olmadan sağlanır.

## <a name="troubleshooting"></a>Sorun giderme

Betik eylemleri tarafından günlüğe kaydedilen bilgi görüntülemek için Ambari web kullanıcı Arabirimi kullanabilirsiniz. Küme oluşturma sırasında komut başarısız olursa, günlükleri kümeyle ilişkili varsayılan depolama hesabı mevcuttur. Bu bölümde hem bu seçenekleri kullanarak günlüklerini alma hakkında bilgi sağlar.

### <a name="using-the-ambari-web-ui"></a>Ambari Web kullanıcı Arabirimi kullanma

1. Tarayıcınızda, https://CLUSTERNAME.azurehdinsight.net için gidin. CLUSTERNAME Hdınsight kümenizin adıyla değiştirin.

    İstendiğinde, küme için yönetici hesabı adını (Yönetici) ve parolasını girin. Bir web formunda yönetici kimlik bilgilerinizi yeniden girmeniz gerekebilir.

2. Sayfanın üstündeki çubuğundan seçin **ops** girişi. Ambari aracılığıyla küme üzerinde gerçekleştirilen işlemler geçerli ve önceki bir listesi görüntülenir.

    ![Seçili ops ile Ambari web kullanıcı Arabirimi çubuğu](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Sahip girişlerini bulmak **çalıştırmak\_customscriptaction** içinde **Operations** sütun. Betik eylemleri çalıştırdığınızda bu girişleri oluşturulur.

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    STDOUT ve STDERR çıktısı görüntülemek için run\customscriptaction girişi seçin ve bağlantılar aracılığıyla detaya. Komut dosyası çalıştığında, bu çıkışı oluşturulur ve yararlı bilgiler içerebilir.

### <a name="access-logs-from-the-default-storage-account"></a>Varsayılan depolama hesabı erişim günlükleri

Küme oluşturma bir betik eylemi hatası nedeniyle başarısız olursa, günlükleri küme depolama hesabından erişilebilir.

* Depolama günlüklerine kullanılabilir `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    Bu dizin altında headnode, workernode ve zookeeper düğümleri için günlükleri ayrı olarak düzenlenir. Bazı örnekler şunlardır:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Çalışan düğümü** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Zookeeper düğümü** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Tüm stdout ve stderr karşılık gelen konağının depolama hesabına karşıya. Bir **çıkış -\*.txt** ve **hataları -\*.txt** her komut dosyası eylemi için. Çıktı *.txt dosya konakta çalışan komut dosyasının URI hakkında bilgi içerir. Örneğin:

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Betik eylemi küme sürekli olarak aynı ada sahip oluşturmak mümkündür. Böyle bir durumda tarih klasör adını temel alarak ilgili günlükleri ayırt edebilirsiniz. Örneğin, farklı tarihlerde oluşturulan bir küme (contoso.com) için klasör yapısı aşağıdaki günlük girdileri benzer görünür:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Aynı gün içinde aynı ada sahip bir komut dosyası eylemi kümesi oluşturursanız, ilgili günlük dosyalarını tanımlamak için benzersiz önek kullanabilirsiniz.

* Bir küme 12: 00'da (gece yarısı) yakın oluşturursanız, günlük dosyaları iki gün boyunca span mümkündür. Böyle durumlarda, aynı küme için iki farklı tarih klasörleri görürsünüz.

* Günlük dosyaları için varsayılan kapsayıcı karşıya yükleme, özellikle büyük kümeleri için 5 dakika kadar sürebilir. Günlüklere erişmek istiyorsanız, bir komut dosyası eylemi başarısız olursa bu nedenle, hemen küme silmemelisiniz.

### <a name="ambari-watchdog"></a>Ambari izleme

> [!WARNING]
> Linux tabanlı Hdınsight kümenizdeki Ambari izleme (hdinsightwatchdog) için parolayı değiştirmeyin. Bu hesabın parolasını değiştirme Hdınsight kümesinde yeni betik eylemleri çalıştırma yeteneğini keser.

### <a name="cant-import-name-blobservice"></a>Ad BlobService içeri aktarılamıyor

__Belirtiler__: betik eylemi başarısız. İşlemi Ambari içinde görüntülediğinizde, aşağıdakine benzer bir metin görüntülenir:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Neden__: Hdınsight kümesi ile birlikte Python Azure Storage istemcisi yükseltirseniz, bu hata oluşur. Hdınsight Azure Storage istemci 0.20.0 bekliyor.

__Çözümleme__: Bu hatayı gidermek için el ile her küme düğümünü kullanarak bağlanma `ssh` ve doğru depolama istemci sürümünü yeniden yüklemek için aşağıdaki komutu kullanın:

```
sudo pip install azure-storage==0.20.0
```

SSH kümeye bağlanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Küme oluşturma sırasında kullanılan komut geçmişi göstermiyor

Kümenizi 15 Mart 2016'dan önce oluşturulduysa, bir giriş betik eylemi geçmişinde göremeyebilirsiniz. 15 Mart 2016'dan sonra kümeyi yeniden boyutlandırmak, bunlar yeni düğümleri yeniden boyutlandırma işlemi bir parçası olarak uygulanır olarak küme oluşturma sırasında kullanarak komut geçmişinde görünür.

İki istisna mevcuttur:

* Kümenizi 1 Eylül 2015 önce oluşturulduysa. Betik eylemleri kullanıma sunulan, bu tarih olur. Bu tarihten önce oluşturulan herhangi bir küme betik eylemleri küme oluşturma için kullanılmamış.

* Birden çok betik eylemleri küme oluşturma sırasında kullanılır ve birden fazla komut dosyası için aynı adı veya aynı adı, aynı URI, ancak farklı parametreler birden fazla komut dosyası için kullanılan istiyorsanız. Bu durumlarda, aşağıdaki hatayı alırsınız:

    Varolan komut dosyalarında çakışan betik adları nedeniyle bu kümede eylemler olabilir yeni betik verdi. Kümesine sağlanan betik adları oluşturmak gereken tüm benzersiz olmalıdır. Varolan komut dosyalarını yeniden boyutlandırma üzerinde verdi.

## <a name="next-steps"></a>Sonraki adımlar

* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions-linux.md)
* [Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install-linux.md)
* [Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install-linux.md)
* [Hdınsight kümesi için ek depolama alanı eklentisi](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Küme oluşturma sırasında aşamaları"
