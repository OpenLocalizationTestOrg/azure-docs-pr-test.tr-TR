---
title: "Resource Manager şablonu ile aaaKey kasası gizli | Microsoft Docs"
description: "Nasıl toopass gizli bir anahtarı dağıtımı sırasında bir parametre olarak kasa gösterir."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Dağıtım sırasında anahtar kasası toopass güvenli parametre değeri kullanma

Dağıtım sırasında parametre olarak toopass (örneğin, parola) güvenli bir değerle gerektiğinde, hello değerinden alabilir bir [Azure anahtar kasası](../key-vault/key-vault-whatis.md). Hello anahtar kasasını ve gizli parametre dosyanıza başvurarak hello değerini alır. anahtar kasası kimliğini yalnızca başvuru olduğundan hello değeri hiçbir zaman kullanıma İhtiyacınız olmayan toomanually hello kaynakları dağıttığınız her zaman için hello gizli anahtar hello değer girin. Merhaba anahtar kasası dağıttığınız hello kaynak grubundan farklı bir abonelik var olabilir. Merhaba anahtar kasası başvururken hello abonelik kimliğini içerir

Merhaba anahtar kasası oluştururken hello ayarlama *enabledForTemplateDeployment* özelliği çok*doğru*. Bu değer tootrue ayarlayarak, Resource Manager şablonlarını dağıtımı sırasında erişimine.  

## <a name="deploy-a-key-vault-and-secret"></a>Bir anahtar kasası ve gizli dağıtma

toocreate bir anahtar kasası ve gizli anahtarı, Azure CLI veya PowerShell kullanın. Bu hello anahtar kasası şablon dağıtım için etkinleştirildiğinde dikkat edin. 

Azure CLI için şunu kullanın:

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

PowerShell için şunu kullanın:

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Erişim toohello gizli etkinleştir

Yeni bir anahtar kasası veya varolan bir kullanıp kullanmadığınızı hello gizli hello şablon dağıtma bu hello kullanıcının erişebildiği emin olun. Gizli başvuruda bulunan bir şablonu dağıtmayı hello kullanıcı hello olmalıdır `Microsoft.KeyVault/vaults/deploy/action` hello anahtar kasası için izni. Merhaba [sahibi](../active-directory/role-based-access-built-in-roles.md#owner) ve [katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#contributor) rolleri hem bu erişimi verin. Ayrıca bir [özel rol](../active-directory/role-based-access-control-custom-roles.md) , bu izni verir ve hello kullanıcı toothat rolünü ekleyin. Bir kullanıcı tooa rolü ekleme hakkında daha fazla bilgi için bkz: [tooadministrator rolleri Azure Active Directory'de bir kullanıcı atamak](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Statik Kimliğine sahip bir gizlilik başvurusu

bir anahtar kasası gizli alan hello gibi herhangi bir şablonu şablonudur. Çünkü **hello anahtar kasası hello parametre dosyasında değil hello şablon başvurusu.** Örneğin, bir yönetici parolası içeren bir SQL veritabanı şablonu aşağıdaki hello dağıtır. Merhaba parola parametresi tooa güvenli dize ayarlanır. Ancak, bu değeri nereden geldiğini hello şablon belirtmiyor.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

Şimdi, şablon önceki hello için bir parametre dosyası oluşturun. Merhaba parametre dosyasında hello şablon hello parametresinde hello adıyla eşleşen bir parametre belirtin. Merhaba parametre değeri için hello hello anahtar Kasası'nı gizli başvuru. Merhaba kaynak tanımlayıcısı hello anahtar kasasının ve hello gizli hello adını geçirerek hello gizli başvuru. Merhaba, aşağıdaki örneğine hello anahtar kasasına gizli anahtarı zaten mevcut olmalıdır ve kendi kaynak kimliği için statik bir değer girin

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Dinamik Kimliğine sahip bir gizlilik başvurusu

başlangıç anahtarı için bir statik kaynak kimliği toopass gizli nasıl kasa Hello önceki bölümde gösterilmiştir. Ancak, bazı senaryolarda tooreference hello geçerli dağıtımda göre değişen bir anahtar kasası gizli anahtarı gerekir. Bu durumda, sabit kodlu hello kaynak kimliği hello Parametreler dosyasında yapamazsınız. Ne yazık ki, şablon ifadeleri hello parametreleri dosyada izin verilmez çünkü hello Parametreler dosyasında hello kaynak kimliği dinamik olarak oluşturulamıyor.

toodynamically hello kaynak kimliği için bir anahtar kasası gizli anahtar oluşturmak, iç içe geçmiş bir şablona hello gizli gereken hello kaynak taşımanız gerekir. Ana şablonunuzda hello iç içe geçmiş şablonuna ekleme ve dinamik olarak üretilen hello kaynak kimliği içeren bir parametre geçirin

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Sonraki adımlar
* Anahtar kasalarını hakkında genel bilgi için bkz: [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md).
* Anahtar parolaları başvuran tüm örnekler için bkz: [anahtar kasası örnekler](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

