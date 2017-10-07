---
title: "aaaCreate Hadoop kümeleri şablonları - Azure Hdınsight kullanarak | Microsoft Docs"
description: "Resource Manager şablonları kullanarak toocreate Hdınsight için nasıl kümeleri öğrenin"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Resource Manager şablonları kullanarak Hdınsight'ta Hadoop kümeleri oluşturma
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Bu makalede, çeşitli yollar hakkında bilgi edineceksiniz toocreate Azure Hdınsight kümeleri ile Azure Resource Manager şablonları. Daha fazla bilgi için bkz: [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](../azure-resource-manager/resource-group-template-deploy.md). diğer küme oluşturma araçları ve özellikleri hakkında toolearn tıklatın hello sekme seçicisini hello üstteki bu sayfa ya da bakın [küme oluşturma yöntemleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Bu makaledeki toofollow hello yönergeleri, ihtiyacınız vardır:

* Bir [Azure aboneliği](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Azure PowerShell ve/veya Azure CLI.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Resource Manager şablonları
Resource Manager şablonu tek ve eşgüdümlü bir işlemle, uygulamanız için aşağıdaki kolay toocreate hello kolaylaştırır:
* Hdınsight kümeleri ile bağımlı kaynakları (Merhaba varsayılan depolama hesabı gibi)
* Diğer kaynaklar (örneğin, Azure SQL veritabanı toouse Apache Sqoop)

Merhaba şablonunda hello uygulama için gerekli olan hello kaynakları tanımlayın. Ayrıca, farklı ortamlar için dağıtım parametreleri tooinput değerleri de belirtin. JSON ve dağıtımınız için tooconstruct değerleri kullanan ifadelerin Hello şablonu oluşur.

Hdınsight şablon örnekleri konumunda bulabilirsiniz [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/?term=hdinsight). Platformlar arası kullanmak [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) hello ile [Resource Manager uzantısını](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) veya bir metin düzenleyicisi toosave hello şablonu istasyonunuzda bir dosyaya. Nasıl toocall hello şablonu farklı yöntemler kullanarak öğrenin.

Resource Manager şablonları hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Yazar Azure Resource Manager şablonları](../azure-resource-manager/resource-group-authoring-templates.md)
* [Bir uygulamayı Azure Resource Manager şablonları ile dağıtma](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Şablonları oluştur

Hello Azure portal kullanarak, bir kümenin tüm hello özelliklerini yapılandırmak ve hello şablonunun dağıtmadan önce kaydedin. Merhaba şablon daha sonra yeniden kullanabilirsiniz.

**toogenerate hello Azure portal kullanarak bir şablonu**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **yeni** hello sol menüsünde **Intelligence + analiz**ve ardından **Hdınsight**.
3. Merhaba yönergeleri tooenter özellikleri izleyin. Her iki hello kullanabilirsiniz **hızlı Oluştur** veya hello **özel** seçeneği.
4. Merhaba üzerinde **Özet** sekmesini tıklatın, **karşıdan şablonu ve parametre**:

    ![Hdınsight Hadoop kümesi Resource Manager şablonu indirme oluşturma](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    Hello şablon dosyası, parametreleri dosyasını ve kod kullanılan örneklerin toodeploy hello şablon listesini bakın:

    ![Hdınsight Hadoop Resource Manager şablonu indirme seçeneklerini küme oluşturma](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    Buradan, hello şablonunu indirebilir, tooyour Şablon kitaplığı Kaydet veya hello şablonunu dağıtın.

    tooaccess kitaplığınızda, bir şablon tıklatın **daha fazla hizmet** hello sol menüsünden ve ardından **şablonları** (Merhaba altında **diğer** kategori).

    > [!Note]
    > Merhaba şablonu ve parametre dosyası birlikte kullanılması gerekir. Aksi takdirde, beklenmedik sonuçlar alabilirsiniz. Örneğin, varsayılan hello **clusterKind** özellik değeri olduğundan her zaman **hadoop**, hello şablon indirmeden önce hangi rağmen belirttiğiniz.



## <a name="deploy-with-powershell"></a>PowerShell ile dağıtma

Bu yordam, Hdınsight'ta Hadoop kümesi oluşturur.

1. Hello Hello JSON dosyasını kaydedin [ek](#appx-a-arm-template) tooyour iş istasyonu. Hello PowerShell Betiği, hello dosya adıdır `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. Merhaba parametreler ve değişkenler gerekirse ayarlayın.
3. PowerShell Betiği aşağıdaki hello kullanarak Hello şablon çalıştırın:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    Merhaba PowerShell komut dosyası yalnızca hello küme adını yapılandırır. Merhaba şablonu sabit kodlanmış Hello depolama hesap adı değil. İstendiğinde tooenter hello küme kullanıcı parolası var. (Merhaba varsayılan kullanıcı adı **yönetici**.) Ayrıca istendiğinde tooenter hello SSH kullanıcı parolası var. (Merhaba varsayılan SSH kullanıcı adı **sshuser**.)  

Daha fazla bilgi için bkz: [PowerShell ile dağıtma](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>CLI ile dağıtma
Aşağıdaki örnek hello Azure komut satırı arabirimi (CLI) kullanır. Bir küme, bağımlı depolama hesabı ve kapsayıcı Resource Manager şablonu çağırarak oluşturur:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

İstendiğinde tooenter şunlardır:
* Merhaba küme adı.
* Merhaba küme kullanıcı parolası. (Merhaba varsayılan kullanıcı adı **yönetici**.)
* Merhaba SSH kullanıcı parolası. (Merhaba varsayılan SSH kullanıcı adı **sshuser**.)

Satır içi parametreleri koddan hello sağlar:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>REST API Hello ile dağıtma
Bkz: [hello REST API ile dağıtma](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Visual Studio ile dağıtma
 Visual Studio toocreate bir kaynak grubu projesi kullanabilir ve tooAzure hello kullanıcı arabirimi aracılığıyla dağıtabilirsiniz. Projenizde kaynakları tooinclude hello türünü seçin. Bu kaynakları toohello Resource Manager şablonu otomatik olarak eklenir. Merhaba proje bir PowerShell komut dosyası toodeploy hello şablonu da sağlar.

Bir giriş toousing için Visual Studio kaynak gruplarıyla, bkz: [Visual Studio üzerinden Azure kaynak gruplarını oluşturma ve dağıtma](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, çeşitli yolları toocreate Hdınsight kümesi öğrendiniz. toolearn daha makaleler hello bakın:

* Kaynaklara hello .NET istemci kitaplığı aracılığıyla dağıtmaya ilişkin bir örnek için bkz: [kaynakları .NET kitaplıkları ve bir şablon kullanarak dağıtmak](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Bir uygulama dağıtımının ayrıntılı örneği için bkz: [sağlamak ve mikro beklendiği azure'da dağıtmak](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Çözüm toodifferent ortamlarınızın dağıtma ile ilgili yönergeler için bkz: [Microsoft Azure geliştirme ve test ortamlarında](../solution-dev-test-environments.md).
* toolearn hello Azure Resource Manager şablonu hello bölümlerini hakkında bkz [şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).
* Bir Azure Resource Manager şablonunda kullanabileceğiniz hello işlevleri bir listesi için bkz: [şablon işlevleri](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Ek: Resource Manager şablonu toocreate Hadoop kümesi
Merhaba aşağıdaki Azure Resource Manager şablonu Linux tabanlı Hadoop kümesi ile Merhaba bağımlı Azure depolama hesabı oluşturur.

> [!NOTE]
> Bu örnek Hive meta depo ve Oozie meta depo için yapılandırma bilgilerini içerir. Merhaba bölümü kaldırmak veya hello şablonunu kullanmadan önce hello bölüm yapılandırın.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Ek: Resource Manager şablonu toocreate bir Spark kümesi

Bu bölümde bir Resource Manager şablonu toocreate Hdınsight Spark kümesinde kullanabilirsiniz. Bu şablon için yapılandırmaları içerir `spark-defaults` ve `spark-thrift-sparkconf` (Spark 1.6 kümelerinde için) ve `spark2-defaults` ve `spark2-thrift-sparkconf` (Spark 2 kümeleri için). Ayrıca toothis, Hdınsight hesaplar ve yapılandırmaları gibi ayarlar `spark.executor.instances`, `spark.executor.memory`, ve `spark.executor.cores` hello küme boyutuna göre. 

Herhangi bir parametre bir bölümde hello şablona bir parçası olarak ayarlarsanız, Hdınsight değil hesaplamak ve set hello Merhaba, diğer parametreler aynı bölüm. Örneğin, parametre `spark.executor.instances` hello olduğu `spark-defaults` yapılandırma. Başka bir parametre ayarlarsanız (örneğin, `spark.yarn.exector.memoryOverhead`) hello içinde `spark-defaults` yapılandırması, Hdınsight değil hesaplamak ve ayarlama hello `spark.executor.instances` parametresini de.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
