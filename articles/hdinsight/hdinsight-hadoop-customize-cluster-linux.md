---
title: "aaaCustomize betik eylemleri - Azure kullanarak Hdınsight kümelerini | Microsoft Docs"
description: "Betik eylemleri kullanılarak tooLinux tabanlı Hdınsight kümeleri özel bileşenleri ekleyin. Betik eylemleri, kullanılan toocustomize hello küme yapılandırması veya ek hizmetleri ve yardımcı programları ton, Solr veya r gibi ekleme Bash betikleridir"
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme

Hdınsight adlı bir yapılandırma seçeneği sağlar **betik eylemi** hello küme özelleştirme özel komut dosyaları çağırır. Bu komut dosyaları kullanılan tooinstall ek bileşenleridir ve yapılandırma ayarlarını değiştirebilirsiniz. Betik eylemleri, sırasında veya Küme oluşturulduktan sonra kullanılabilir.

> [!IMPORTANT]
> Merhaba özelliği toouse betik eylemleri zaten çalışan bir kümede yalnızca Linux tabanlı Hdınsight kümeleri için mevcut değil.
>
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Betik eylemleri, ayrıca bir Hdınsight uygulaması olarak yayımlanan toohello Azure Marketi olabilir. Bu belgedeki örneklerde hello bazıları, PowerShell ve .NET SDK'sı hello betik eylemi komutları kullanarak bir Hdınsight uygulamasının nasıl yükleyebileceğinizi gösterir. Hdınsight uygulamaları hakkında daha fazla bilgi için bkz: [hello Azure Marketi'nde yayımlama Hdınsight uygulamalarınızı](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>İzinler

Bir etki alanına katılmış Hdınsight kümesi kullanıyorsanız, betik eylemleri ile Merhaba kümesi kullanırken gerekli olan iki Ambari izinleri vardır:

* **AMBARI. ÇALIŞTIRMA\_özel\_KOMUTU**: Merhaba Ambari Yönetici rolü varsayılan olarak bu izne sahiptir.
* **KÜME. ÇALIŞTIRMA\_özel\_KOMUTU**: her ikisi de Hdınsight küme yöneticisinin hello ve Ambari yönetici varsayılan olarak bu izne sahip.

İzinleri etki alanına katılmış Hdınsight ile çalışma hakkında daha fazla bilgi için bkz: [etki alanına katılmış Hdınsight kümelerini yönetme](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Erişim denetimi

Azure aboneliğiniz hello Yöneticisi/sahibi değilseniz, hesabınızın en az olmalı **katkıda bulunan** hello Hdınsight kümesi içeren erişim toohello kaynak grubu.

Ayrıca, Hdınsight kümesi, birisi ile en az oluşturuyorsanız **katkıda bulunan** erişim toohello Azure aboneliği gerekir daha önce kaydettiğiniz Hdınsight için hello sağlayıcısı. Katkıda bulunan erişim toohello aboneliği olan bir kullanıcı ilk kez hello abonelikte hello için bir kaynak oluşturduğunda sağlayıcı kaydı olur. Bu işlem ayrıca [REST ile bir sağlayıcı kaydedilerek](https://msdn.microsoft.com/library/azure/dn790548.aspx) kaynak oluşturulmadan gerçekleştirilebilir.

Erişim yönetimi ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hello Azure portalına erişim yönetimi kullanmaya başlama](../active-directory/role-based-access-control-what-is.md)
* [Rol atamaları toomanage erişim tooyour Azure aboneliği kaynakları kullanın](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Anlama betik eylemleri

Bir komut dosyası yalnızca bir URI sağlayın Bash komut dosyası ve parametreleri bir eylemdir. Merhaba Hdınsight küme düğümlerinde Hello komut dosyasını çalıştırır. özellikleri ve betik eylemleri özelliklerini Hello aşağıda verilmiştir.

* Merhaba Hdınsight kümeden erişilebilir olduğunu URI üzerinde depolanmalıdır. Merhaba, olası depolama konumları şunlardır:

    * Bir **Azure Data Lake Store** hello Hdınsight küme tarafından erişilebilir olan hesap. Hdınsight ile Azure Data Lake Store hakkında daha fazla bilgi için bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Data Lake Store'da depolanan bir komut dosyası, hello URI biçimi kullanıldığında `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Merhaba hizmet asıl Hdınsight kullandığı tooaccess Data Lake Store okuma erişimi toohello komut dosyası olması gerekir.

    * Bir blobu bir **Azure depolama hesabı** hello Hdınsight kümesi için herhangi bir hello birincil ya da ek depolama hesabı olmasıdır. Hdınsight küme oluşturma sırasında depolama hesapları bu tür erişim tooboth verilir.

    * Paylaşım Hizmeti Azure Blob, GitHub, OneDrive, Dropbox, vb. gibi ortak bir dosya.

        Örneğin URI, bakın hello [örnek betik eylemi betikler](#example-script-action-scripts) bölümü.

        > [!WARNING]
        > Hdınsight yalnızca destekler __genel amaçlı__ Azure depolama hesapları. Merhaba şu anda desteklemiyor __Blob storage__ hesap türü.

* Çok kısıtlanabilir**yalnızca belirli düğüm türleri üzerinde çalıştırmak**örnek baş düğümler ve çalışan düğümleri için.

  > [!NOTE]
  > Hdınsight Premium ile birlikte kullanıldığında, hello betik hello kenar düğümüne kullanılması gerektiğini belirtebilirsiniz.

* Olabilir **kalıcı** veya **geçici**.

    **Kalıcı** betiklerdir uygulanan tooworker düğümleri eklenen toohello küme hello betik çalıştıktan sonra. Örneğin, Hello küme ölçeklendirme.

    Kalıcı bir betik bir baş düğüm gibi değişiklikler tooanother düğüm türü de geçerli.

  > [!IMPORTANT]
  > Kalıcı betik eylemleri benzersiz bir ad olmalıdır.

    **Geçici** betikleri kalıcı değildir. Sahip Hello betiği çalıştırdıktan sonra bunlar uygulanan tooworker düğümleri eklenen toohello küme olup olmadığı. Sonradan bir geçici kod tooa yükseltebilirsiniz betik kalıcı ya da kalıcı betik tooan geçici betik indirgemek.

  > [!IMPORTANT]
  > Küme oluşturma sırasında kullanılan betik eylemleri otomatik olarak kalıcıdır.
  >
  > Başarısız olmayan betikleri özellikle olması gerektiğini belirtmek olsa bile kalıcı.

* Kabul edebilir **parametreleri** kullanılan hello komut dosyası tarafından yürütme sırasında.
* Çalıştırma **kök düzeyinde ayrıcalıklara** hello küme düğümlerinde.
* Merhaba kullanılabilir **Azure portal**, **Azure PowerShell**, **Azure CLI**, veya **Hdınsight .NET SDK'sı**

Merhaba küme çalıştırdığınız sahip tüm betikler geçmişini tutar. hello geçmişi, yükseltme veya indirgeme işlemleri için bir komut dosyası toofind hello kimliği gerektiğinde kullanışlıdır.

> [!IMPORTANT]
> Hiçbir otomatik şekilde tooundo yoktur hello bir betik eylemi tarafından yapılan değişiklikler. El ile Merhaba değişiklikleri ters ya da bunları tersine çevirir bir komut dosyası sağlar.


### <a name="script-action-in-hello-cluster-creation-process"></a>Betik eylemi hello küme oluşturma işlemi

Küme oluşturma sırasında kullanılan betik eylemleri eylemler var olan bir küme üzerinde çalışan komut dosyasından biraz farklılık gösterir:

* Merhaba komut dosyası **otomatik olarak kalıcı**.
* A **hatası** hello betik hello küme oluşturma işlemi toofail neden olabilir.

Betik eylemi hello oluşturma işlemi sırasında çalıştırıldığında hello Aşağıdaki diyagramda gösterilmektedir:

![Hdınsight küme özelleştirme ve küme oluşturma sırasında aşamaları][img-hdi-cluster-states]

Hdınsight yapılandırılırken hello komut dosyasını çalıştırır. Bu aşamada, tüm paralel hello komut dosyasını çalıştırır hello küme ve kök ayrıcalıklarıyla çalıştırır hello düğümlerde bulunan belirli düğümler hello.

> [!NOTE]
> Merhaba komut dosyası kök düzeyinde ayrıcalığıyla hello küme düğümleri üzerinde çalıştığı için durdurma ve Hadoop ile ilgili hizmetlerin gibi hizmetler başlatma gibi işlemler gerçekleştirebilirsiniz. Hizmetleri durdurursanız, hello komut dosyası çalıştırma tamamlanmadan önce hello ambarı hizmet ve diğer Hadoop ile ilgili hizmetlerin hazır ve çalışır olduğundan emin olmalısınız. Bu hizmetler gerekli toosuccessfully, hello sistem durumu ve hello küme durumunu, oluşturulurken belirler.


Küme oluşturma sırasında aynı anda birden çok betik eylemleri kullanabilirsiniz. Bu komut dosyalarını belirtilmiş olması hello sırayla çağrılır.

> [!IMPORTANT]
> Betik eylemleri, 60 dakika veya zaman aşımı içinde tamamlamanız gerekir. Küme hazırlama sırasında diğer Kurulum ve yapılandırma işlemleri eşzamanlı olarak hello komut dosyasını çalıştırır. CPU süresi veya ağ bant genişliği gibi kaynakları için rekabet geliştirme ortamınızı makinelerinden hello betik tootake uzun toofinish neden olabilir.
>
> toominimize hello alır toorun hello komut dosyası zaman, yükleme ve kaynak uygulamalardan derleme gibi görevleri kaçının. Uygulamaları önceden derleme ve Azure depolama alanına hello ikili depolar.


### <a name="script-action-on-a-running-cluster"></a>Betik eylemi çalıştıran bir kümede

Aksine, bir komut dosyasında hata küme oluşturma sırasında kullanılan eylemler zaten çalışan bir küme üzerinde çalışan komut dosyası otomatik olarak hello küme toochange başarısız tooa durumunun neden olmaz. Bir komut dosyası tamamlandıktan sonra hello küme "çalışır" tooa döndürmelidir.

> [!IMPORTANT]
> Merhaba küme 'çalışıyor' durumu olsa bile hello başarısız betik şeyler kopuk olabilir. Örneğin, bir komut dosyası hello kümenin gerektirdiği dosyaları silebilir.
>
> Tooyour küme uygulamadan önce bir komut dosyası yaptığı anladığınızdan emin olmanız gerekir böylece komut dosyalarını eylemleri kök ayrıcalıkları ile çalıştırın.

Bir komut dosyası tooa küme uygularken toofrom hello küme durumunu değiştirir **çalıştıran** çok**kabul edilen**, ardından **Hdınsight yapılandırma**ve son olarak çok geri**Çalıştıran** başarılı bir komut dosyası. Merhaba betik durum hello betik eylemi geçmişinde günlüğe kaydedilir ve hello komut başarılı veya başarısız olup olmadığını, bu bilgileri toodetermine kullanabilirsiniz. Örneğin, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet'ini bir komut dosyası kullanılan tooview hello durumu olabilir. Metin aşağıdaki bilgileri benzer toohello döndürür:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Merhaba Küme oluşturulduktan sonra hello küme kullanıcı (Yönetici) parolasını değiştirdiyseniz, bu küme karşı eylemler çalışan betik başarısız olabilir. Bu hedef çalışan düğümleri kalıcı betik eylemleri varsa, bu komut dosyalarını hello küme ölçeklendirdiğinizde başarısız olabilir.

## <a name="example-script-action-scripts"></a>Örnek betik eylemi betikler

Betik eylemi betikleri yardımcı programlarını aşağıdaki hello kullanılabilir:

* Azure portalına
* Azure PowerShell
* Azure CLI
* HDInsight .NET SDK'sı

Hdınsight Hdınsight kümelerinde bileşenleri aşağıdaki betikler tooinstall hello sağlar:

| Ad | Betik |
| --- | --- |
| **Bir Azure depolama hesabı ekleme** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.sh. Bkz: [ekle ek depolama alanı tooan Hdınsight kümesi](hdinsight-hadoop-add-storage.md). |
| **Hue yüklemek** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/install-Hue-uber-v02.sh. Bkz: [yükleme ve kullanma ton hdınsight kümeleri](hdinsight-hadoop-hue-linux.md). |
| **Presto yükleyin** |https://RAW.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Bkz: [yükleme ve kullanma Presto hdınsight kümeleri](hdinsight-hadoop-install-presto.md). |
| **Solr yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-installer-v01.sh. Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install-linux.md). |
| **Giraph yükleyin** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install-linux.md). |
| **Ön yük Hıve kitaplıkları** |https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Bkz: [eklemek Hive kitaplıkları Hdınsight kümelerinde](hdinsight-hadoop-add-hive-libraries.md). |
| **Mono yükleme veya güncelleştirme** | https://hdiconfigactions.BLOB.Core.Windows.NET/install-Mono/install-Mono.bash. Bkz: [yükleme veya güncelleştirme Mono hdınsight'ta](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Küme oluşturma sırasında bir betik eylemi kullanın

Bu bölümde, betik eylemleri bir Hdınsight kümesi oluştururken kullanabileceğiniz hello farklı yolları üzerinde örnekler verilmektedir.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Hello Azure Portalı'ndan küme oluşturma sırasında bir betik eylemi kullanın

1. Konusunda açıklandığı gibi bir küme oluşturmaya başlamak [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md). Merhaba ulaştığında Durdur __küme Özet__ bölümü.

2. Merhaba gelen __küme Özet__ bölümü, select hello __Düzenle__ için bağlantı __Gelişmiş ayarları__.

    ![Gelişmiş ayarlar bağlantısı](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Merhaba gelen __Gelişmiş ayarları__ bölümünde, select __betik eylemleri__. Merhaba gelen __betik eylemleri__ bölümünde, select __+ yeni Gönder__

    ![Yeni betik eylemi Gönder](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Kullanım hello __bir komut dosyası seçin__ girişi tooselect önceden yapılmış bir komut dosyası. toouse özel bir komut dosyası seçin __özel__ ve hello sağlamak __adı__ ve __betik URI Bash__ betiği için.

    ![Merhaba select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Aşağıdaki tablonun hello hello öğeleri hello formunda açıklar:

    | Özellik | Değer |
    | --- | --- |
    | Bir komut dosyası seçin | toouse select kendi betiğinizi __özel__. Aksi durumda, sağlanan hello komut dosyalarından birini seçin. |
    | Ad |Merhaba betik eylemi için bir ad belirtin. |
    | Bash betik URI |Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin. |
    | HEAD/çalışan/Zookeeper |Merhaba düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) hangi hello özelleştirme betiğini çalıştırın. |
    | Parametreler |Merhaba komut dosyası için gereken Hello parametreleri belirtin. |

    Kullanım hello __bu betik eylemini Sürdür__ betik hello girişi tooensure ölçeklendirme işlemleri sırasında uygulanır.

5. Seçin __oluşturma__ toosave hello komut dosyası. Daha sonra __+ gönderme yeni__ tooadd başka bir komut dosyası.

    ![Birden çok betik eylemleri](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Komut dosyaları eklemeyi bitirdiğinizde, hello kullan __seçin__ düğmesine tıklayın ve ardından hello __sonraki__ düğmesini tooreturn toohello __küme Özet__ bölümü.

3. toocreate hello küme, select __oluşturma__ hello gelen __küme Özet__ seçim.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Azure Resource Manager şablonları bir betik eylemi kullanın

Bu bölümdeki Hello örnekleri toouse Eylemler Azure Resource Manager şablonları ile nasıl komut dosyası gösterilmektedir.

#### <a name="before-you-begin"></a>Başlamadan önce

* Bir iş istasyonu toorun Hdınsight Powershell cmdlet'leri yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).
* Yönergeler için bkz: toocreate şablonları [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).
* Resource Manager ile daha önce Azure PowerShell kullanmadıysanız, bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Betik eylemi kullanarak kümeleri oluşturma

1. Şablon tooa konumu bilgisayarınızda aşağıdaki hello kopyalayın. Bu şablon Giraph hello kümedeki hello headnodes ve çalışan düğümlere yükler. Merhaba JSON şablonunu geçerli olduğunu da doğrulayabilirsiniz. Şablonunuzu içerik içine yapıştırma [JSONLint](http://jsonlint.com/), bir çevrimiçi JSON doğrulama aracı.

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
2. Azure PowerShell'i başlatın ve Azure hesabı tooyour içinde oturum. Kimlik bilgilerinizi girdikten sonra hello komut, hesabınız hakkında bilgiler döndürür.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Merhaba abonelik kimliği sağlayın, birden çok aboneliğiniz varsa dağıtım için toouse istiyor.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Kullanabileceğiniz `Get-AzureRmSubscription` tooget hello abonelik kimliği her biri için içerir hesabınızla ilişkili tüm Aboneliklerin listesini.

4. Varolan bir kaynak grubu yoksa, bir kaynak grubu oluşturun. Merhaba kaynak grubunu ve çözümünüz için gereksinim duyduğunuz konumu Hello adını sağlayın. Merhaba yeni kaynak grubu özetini döndürülür.

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

5. toocreate hello çalıştırmak kaynak grubunuz için bir dağıtım **New-AzureRmResourceGroupDeployment** komut ve hello gerekli parametreleri belirtin. Merhaba parametreler veri aşağıdaki hello şunları içerir:

    * Dağıtımınız için bir ad
    * Kaynak grubunuzun Hello adı
    * Merhaba yolu veya URL'si toohello şablonu oluşturduğunuz.

  Şablonunuzu herhangi bir parametre gerektiriyorsa, bu parametreler de geçmesi gerekir. Bu durumda, hello betik eylemi tooinstall R hello kümedeki herhangi bir parametre gerektirmez.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    İstendiğinde tooprovide hello şablonda tanımlanan hello parametreler için değerler.

1. Merhaba kaynak grubu dağıtıldığında hello dağıtımının bir özeti görüntülenir.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Dağıtımınızı başarısız olursa, aşağıdaki cmdlet'leri tooget bilgilerle hello hataları hakkında hello kullanabilirsiniz.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Azure PowerShell üzerinden küme oluşturma sırasında bir betik eylemi kullanın

Bu bölümde, hello kullanırız [Ekle AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) betik eylemi toocustomize bir küme kullanarak cmdlet tooinvoke komut dosyaları. Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun. Bir iş istasyonu toorun Hdınsight PowerShell cmdlet'leri yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).

Merhaba aşağıdaki komut dosyası gösterilmektedir nasıl tooapply PowerShell kullanarak bir küme oluştururken bir betik eylemi:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Merhaba küme oluşturulmadan önce birkaç dakika sürebilir.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Merhaba Hdınsight .NET SDK'sı öğesinden küme oluşturma sırasında bir betik eylemi kullanın

Merhaba Hdınsight .NET SDK'sı bir .NET uygulamasında Hdınsight ile daha kolay toowork kolaylaştırır istemci kitaplıkları sağlar. Kod örneği için bkz: [.NET SDK kullanarak Hdınsight'ta oluşturma Linux tabanlı kümelerde hello](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Küme çalışan betik eylemi tooa Uygula

Bu bölümde, nasıl tooapply betik çalıştıran küme eylemleri tooa öğrenin.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Küme hello Azure portal ' çalışan betik eylemi tooa Uygula

1. Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.

2. Merhaba Hdınsight küme genel bakış'tan, hello seçin **betik eylemleri** döşeme.

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** hello ayarları bölümünün gelen.

3. Merhaba betik eylemleri bölümünde Hello üstten seçin **gönderme yeni**.

    ![Küme çalışan bir komut dosyası tooa Ekle](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Kullanım hello __bir komut dosyası seçin__ girişi tooselect önceden yapılmış bir komut dosyası. toouse özel bir komut dosyası seçin __özel__ ve hello sağlamak __adı__ ve __betik URI Bash__ betiği için.

    ![Merhaba select komut dosyası biçiminde bir komut dosyası ekleme](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Aşağıdaki tablonun hello hello öğeleri hello formunda açıklar:

    | Özellik | Değer |
    | --- | --- |
    | Bir komut dosyası seçin | toouse select kendi betiğinizi __özel__. Aksi durumda, sağlanan komut dosyasını seçin. |
    | Ad |Merhaba betik eylemi için bir ad belirtin. |
    | Bash betik URI |Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin. |
    | HEAD/çalışan/Zookeeper |Merhaba düğüm belirtin (**Head**, **çalışan**, veya **ZooKeeper**) hangi hello özelleştirme betiğini çalıştırın. |
    | Parametreler |Merhaba komut dosyası için gereken Hello parametreleri belirtin. |

    Kullanım hello __bu betik eylemini Sürdür__ girişi toomake emin hello betik ölçeklendirme işlemleri sırasında uygulanır.

5. Son olarak, hello kullan **oluşturma** düğmesini tooapply hello betik toohello küme.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Küme Azure Powershell'den çalışan betik eylemi tooa Uygula

Devam etmeden önce Azure PowerShell'i yükleyip yapılandırdığınızdan emin olun. Bir iş istasyonu toorun Hdınsight PowerShell cmdlet'leri yapılandırma hakkında daha fazla bilgi için bkz: [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview).

Merhaba aşağıdaki örnekte gösterilmiştir nasıl tooapply bir betik eylemi tooa çalışan küme:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Merhaba işlemi tamamlandığında, metin aşağıdaki bilgileri benzer toohello alırsınız:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Küme hello Azure CLI ' çalışan betik eylemi tooa Uygula

Devam etmeden önce hello Azure CLI yükleyip yapılandırdığınızdan emin olun. Daha fazla bilgi için bkz: [yükleme hello Azure CLI](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooswitch tooAzure Resource Manager moduna komutu hello komut satırında aşağıdaki hello kullan:

        azure config mode arm

2. Tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullanın.

        azure login

3. Küme çalışan bir komut dosyası eylemi tooa komutu tooapply aşağıdaki hello kullanın

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    Bu komutun parametresini atlarsanız, bunlar için istenir. Varsa hello belirttiğiniz ile komut dosyası `-u` belirtebilirsiniz parametreleri kabul hello kullanarak bunları `-p` parametresi.

    Geçerli düğüm türleri `headnode`, `workernode`, ve `zookeeper`. Merhaba betik uygulanan toomultiple düğüm türleri gerekiyorsa, belirtin hello türleri tarafından ayrılmış bir ';'. Örneğin, `-n headnode;workernode`.

    toopersist Merhaba komut dosyası, hello eklemek `--persistOnSuccess`. Ayrıca hello betik daha sonra kullanarak kalıcı `azure hdinsight script-action persisted set`.

    Merhaba işi tamamlandığında, çıkış benzer toohello metin aşağıdaki alırsınız:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>REST API kullanarak küme çalışan betik eylemi tooa Uygula

Bkz: [çalıştırmak betik eylemleri çalıştıran bir kümede](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Küme hello Hdınsight .NET SDK ' çalışan betik eylemi tooa Uygula

Merhaba .NET SDK'sı tooapply betikleri tooa küme kullanarak bir örnek için bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Betik eylemleri indirgemek geçmişini görüntülemek ve Yükselt

### <a name="using-hello-azure-portal"></a>Hello Azure portalını kullanma

1. Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.

2. Merhaba Hdınsight küme genel bakış'tan, hello seçin **betik eylemleri** döşeme.

    ![Betik eylemleri döşeme](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Öğesini de seçebilirsiniz **tüm ayarları** ve ardından **betik eylemleri** hello ayarları bölümünün gelen.

4. Bu küme için komut geçmişini hello betik eylemleri bölüm üzerinde görüntülenir. Bu bilgiler kalıcı komut listesini içerir. Merhaba ekran görüntüsünde, betiği bırakıldı Solr bu küme üzerinde çalışan bu hello görebilirsiniz. Merhaba ekran kalıcı herhangi bir komut dosyası göstermez.

    ![Betik eylemleri bölümünde](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Bir komut dosyası hello geçmişinden seçerek bu komut dosyası için hello özellikleri bölümünde görüntülenir. Merhaba ekranında Hello üstten hello betiği yeniden çalıştırın ya da bunu yükseltin.

    ![Betik eylemleri özellikleri](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Merhaba de kullanabilirsiniz **... ** hello betik eylemleri bölümünde tooperform Eylemler girişlerde sağında toohello.

    ![Eylemler... komut dosyası kullanımı](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Azure PowerShell’i kullanma

| Merhaba aşağıdaki kullanın... | çok... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Kalıcı betik eylemleri hakkında bilgi alma |
| Get-AzureRmHDInsightScriptActionHistory |Komut dosyası uygulanan eylemler toohello küme ya da belirli bir komut dosyası ayrıntılarını geçmişini alma |
| Set-AzureRmHDInsightPersistedScriptAction |Bir geçici yükseltir betik eylemi tooa kalıcı betik eylemi |
| Remove-AzureRmHDInsightPersistedScriptAction |Kalıcı betik eylemi tooan geçici eylem indirger |

> [!IMPORTANT]
> Kullanarak `Remove-AzureRmHDInsightPersistedScriptAction` hello eylemlerin bir komut dosyası tarafından geri almaz. Bu cmdlet, yalnızca hello kalıcı bayrağını kaldırır.

Örnek komut dosyası izleyen hello hello cmdlet'leri toopromote kullanarak gösterir, ardından bir komut dosyası indirgemek.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Hello Azure CLI kullanma

| Merhaba aşağıdaki kullanın... | çok... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Kalıcı betik eylemlerin bir listesini alma |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Belirli kalıcı betik eylemi hakkında bilgi alma |
| `azure hdinsight script-action history list <clustername>` |Komut dosyası uygulanan eylemler toohello küme geçmişini alma |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Bir özel betik eylemi hakkında bilgi alma |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Bir geçici yükseltir betik eylemi tooa kalıcı betik eylemi |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Kalıcı betik eylemi tooan geçici eylem indirger |

> [!IMPORTANT]
> Kullanarak `azure hdinsight script-action persisted delete` hello eylemlerin bir komut dosyası tarafından geri almaz. Bu cmdlet, yalnızca hello kalıcı bayrağını kaldırır.

### <a name="using-hello-hdinsight-net-sdk"></a>Merhaba Hdınsight .NET SDK'yı kullanma

Merhaba .NET SDK'sı tooretrieve betik geçmişi bir kümeden kullanma örneği için yükseltmek veya betikleri indirgemek, bkz: [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Bu örnek ayrıca .NET SDK kullanarak bir Hdınsight uygulaması tooinstall hello nasıl gösterir.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Hdınsight kümelerinde kullanılan açık kaynaklı yazılım desteği

Merhaba Microsoft Azure Hdınsight hizmeti, açık kaynaklı teknolojileri Hadoop biçimlendirilmiş bir ekosistemi kullanır. Microsoft Azure, açık kaynaklı teknolojileri için genel düzeyde desteği sağlar. Merhaba daha fazla bilgi için bkz: **destek kapsamı** hello bölümünü [Azure destek SSS Web sitesine](https://azure.microsoft.com/support/faq/). Merhaba Hdınsight hizmeti yerleşik bileşenleri için destek, ek bir düzeyi sağlar.

Merhaba Hdınsight hizmeti açık kaynak bileşenlerini iki tür vardır:

* **Yerleşik bileşenlerini** -bu bileşenler Hdınsight kümelerinde önceden yüklenmiş ve hello küme çekirdek işlevselliğini sağlar. Örneğin, YARN ResourceManager, hello Hive sorgu dili (HiveQL) ve hello Mahout kitaplık toothis kategori ait. Küme bileşenlerin tam bir listesi kullanılabilir [hello Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).
* **Özel bileşenler** -, hello küme, bir kullanıcı olarak yükleyebilir veya herhangi bir bileşeni hello topluluk bulunan ya da sizin tarafınızdan oluşturulan, iş yükü kullanın.

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenmektedir. Microsoft Support tooisolate yardımcı olur ve sorunları ilgili toothese bileşenler çözümlenemiyor.
>
> Özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Bunlar tooengage kullanılabilir kanalları hello açık kaynak teknolojileri için bu teknoloji derin uzmanlık bulunduğu isteyebilir veya Microsoft desteği mümkün tooresolve hello sorunu olabilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).

Merhaba Hdınsight hizmeti toouse özel bileşenleri çeşitli yöntemler sağlar. Merhaba, nasıl bir bileşen kullanılan veya hello kümeye yüklü bakılmaksızın aynı düzeyde desteği uygular. Merhaba aşağıdaki listede açıklanmaktadır hello en yaygın şekilde özel bileşenlerin kullanılabilir Hdınsight kümelerinde:

1. İş gönderme - Hadoop veya diğer tür execute veya özel bileşenleri kullanan işi gönderilen toohello kümesi olabilir.

2. Küme özelleştirme - küme oluşturma sırasında ek ayarlar ve hello küme düğümlerinde yüklü özel bileşenleri belirtebilirsiniz.

3. Örnekler - popüler özel bileşenleri, Microsoft ve diğerleri için bu bileşenlerin hello Hdınsight kümelerinde nasıl kullanılabileceğini örnek sağlayabilir. Bu örnekler desteği olmadan sağlanır.

## <a name="troubleshooting"></a>Sorun giderme

Betik eylemleri tarafından günlüğe kaydedilen Ambari web kullanıcı Arabirimi tooview bilgi kullanabilirsiniz. Küme oluşturma sırasında Hello komut başarısız olursa, hello günlükleri hello kümesi ile ilişkili hello varsayılan depolama hesabı mevcuttur. Bu bölümde, nasıl tooretrieve hello hem bu seçenekleri kullanarak oturum açtığında bilgileri sağlar.

### <a name="using-hello-ambari-web-ui"></a>Merhaba Ambari Web kullanıcı arabirimini kullanarak

1. Tarayıcınızda, toohttps://CLUSTERNAME.azurehdinsight.net gidin. CLUSTERNAME hello Hdınsight kümenizin adıyla değiştirin.

    İstendiğinde, hello küme için hello yönetici hesabı adını (Yönetici) ve parolasını girin. Bir web formunda tooreenter hello yönetici kimlik bilgilerine sahip olabilir.

2. Merhaba hello sayfanın üst kısmındaki hello Hello çubuğundan seçin **ops** girişi. Ambari aracılığıyla hello kümede gerçekleştirilen geçerli ve önceki işlemleri listesi görüntülenir.

    ![Seçili ops ile Ambari web kullanıcı Arabirimi çubuğu](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Bul hello girişlerine sahip **çalıştırmak\_customscriptaction** hello içinde **Operations** sütun. Merhaba betik eylemleri çalıştırdığınızda bu girişleri oluşturulur.

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT ve STDERR çıktısı hello run\customscriptaction girişi seçin ve hello bağlantılar aracılığıyla detaya. Merhaba komut dosyası çalıştığında, bu çıkışı oluşturulur ve yararlı bilgiler içerebilir.

### <a name="access-logs-from-hello-default-storage-account"></a>Merhaba varsayılan depolama hesabı erişim günlükleri

Merhaba küme oluşturma tooa betik eylemi hatası başarısız olursa, hello günlükleri hello küme depolama hesabından erişilebilir.

* Merhaba depolama günlüklerine kullanılabilir `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![İşlemlerinin ekran görüntüsü](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    Bu dizin altında headnode, workernode ve zookeeper düğümleri hello günlükleri ayrı olarak düzenlenir. Bazı örnekler şunlardır:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Çalışan düğümü** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Zookeeper düğümü** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Tüm stdout ve stderr hello karşılık gelen konağının toohello depolama hesabı karşıya yüklendi. Bir **çıkış -\*.txt** ve **hataları -\*.txt** her komut dosyası eylemi için. Merhaba çıkış *.txt dosya hello konakta çalışan hello betik hello URI hakkında bilgiler içerir. Örneğin:

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Betik eylemi küme sürekli ile Merhaba oluşturmak mümkündür aynı adı. Böyle bir durumda hello tarih klasör adını temel alarak hello ilgili günlükleri ayırt edebilirsiniz. Örneğin, farklı tarihlerde oluşturulan bir küme (contoso.com) hello klasör yapısını günlük girişlerini aşağıdaki benzer toohello görünür:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Merhaba ile bir betik eylemi kümesi oluşturursanız, aynı hello üzerinde aynı adı günü, başlangıç benzersiz önek tooidentify hello ilgili günlük dosyalarını kullanabilirsiniz.

* Bir küme 12: 00'da (gece yarısı) yakın oluşturursanız, hello günlük dosyaları iki gün boyunca span mümkündür. Böyle durumlarda, gördüğünüz Merhaba için iki farklı tarih klasörleri aynı küme.

* Karşıya yükleme günlük dosyalarını toohello varsayılan kapsayıcı yukarı özellikle büyük kümeleri için too5 dakika sürebilir. Tooaccess hello günlükleri istiyorsanız, bir komut dosyası eylemi başarısız olursa bu nedenle, hemen hello küme silmemelisiniz.

### <a name="ambari-watchdog"></a>Ambari izleme

> [!WARNING]
> Linux tabanlı Hdınsight kümenizdeki hello Ambari izleme (hdinsightwatchdog) Hello parolasını değiştirmeyin. Bu hesap için başlangıç parolası değiştiriliyor hello özelliği toorun yeni betik eylemleri hello Hdınsight kümesinde keser.

### <a name="cant-import-name-blobservice"></a>Ad BlobService içeri aktarılamıyor

__Belirtiler__: Merhaba betik eylemi başarısız. Ambari içinde hello işlemi görüntülediğinizde metin benzer toohello aşağıdaki hata görüntülenir:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Neden__: Merhaba Hdınsight kümesi ile birlikte hello Python Azure Storage istemcisi yükseltirseniz, bu hata oluşur. Hdınsight Azure Storage istemci 0.20.0 bekliyor.

__Çözümleme__: tooresolve bu hatayı tooeach küme düğümünü kullanarak el ile bağlanmanız `ssh` ve kullanım hello aşağıdaki komut tooreinstall hello doğru depolama istemci sürümü:

```
sudo pip install azure-storage==0.20.0
```

SSH ile bağlantı toohello kümesi hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Küme oluşturma sırasında kullanılan komut geçmişi göstermiyor

Kümenizi 15 Mart 2016'dan önce oluşturulduysa, bir giriş betik eylemi geçmişinde göremeyebilirsiniz. 15 Mart 2016'dan sonra hello küme yeniden boyutlandırma uygulandıkları gibi küme oluşturma sırasında kullanarak hello komut geçmişinde hello bir parçası olarak hello kümedeki toonew düğümler yeniden boyutlandırma işlemi görünür.

İki istisna mevcuttur:

* Kümenizi 1 Eylül 2015 önce oluşturulduysa. Betik eylemleri kullanıma sunulan, bu tarih olur. Bu tarihten önce oluşturulan herhangi bir küme betik eylemleri küme oluşturma için kullanılmamış.

* Küme oluşturma sırasında birden çok betik eylemleri kullandıysanız ve aynı birden fazla komut dosyası için bir ad verin veya hello hello kullanılan aynı adı, birden fazla komut dosyası için farklı parametreler ancak aynı URI. Bu durumlarda, aşağıdaki hata hello alırsınız:

    Varolan komut dosyalarında tooconflicting betik adları nedeniyle bu kümede eylemler olabilir yeni betik verdi. Kümesine sağlanan betik adları oluşturmak gereken tüm benzersiz olmalıdır. Varolan komut dosyalarını yeniden boyutlandırma üzerinde verdi.

## <a name="next-steps"></a>Sonraki adımlar

* [Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions-linux.md)
* [Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install-linux.md)
* [Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install-linux.md)
* [Ek depolama alanı tooan Hdınsight kümesi Ekle](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Küme oluşturma sırasında aşamaları"
