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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="9ae97-103">Dağıtım sırasında anahtar kasası toopass güvenli parametre değeri kullanma</span><span class="sxs-lookup"><span data-stu-id="9ae97-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="9ae97-104">Dağıtım sırasında parametre olarak toopass (örneğin, parola) güvenli bir değerle gerektiğinde, hello değerinden alabilir bir [Azure anahtar kasası](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ae97-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="9ae97-105">Hello anahtar kasasını ve gizli parametre dosyanıza başvurarak hello değerini alır.</span><span class="sxs-lookup"><span data-stu-id="9ae97-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="9ae97-106">anahtar kasası kimliğini yalnızca başvuru olduğundan hello değeri hiçbir zaman kullanıma</span><span class="sxs-lookup"><span data-stu-id="9ae97-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="9ae97-107">İhtiyacınız olmayan toomanually hello kaynakları dağıttığınız her zaman için hello gizli anahtar hello değer girin.</span><span class="sxs-lookup"><span data-stu-id="9ae97-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="9ae97-108">Merhaba anahtar kasası dağıttığınız hello kaynak grubundan farklı bir abonelik var olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ae97-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="9ae97-109">Merhaba anahtar kasası başvururken hello abonelik kimliğini içerir</span><span class="sxs-lookup"><span data-stu-id="9ae97-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="9ae97-110">Merhaba anahtar kasası oluştururken hello ayarlama *enabledForTemplateDeployment* özelliği çok*doğru*.</span><span class="sxs-lookup"><span data-stu-id="9ae97-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="9ae97-111">Bu değer tootrue ayarlayarak, Resource Manager şablonlarını dağıtımı sırasında erişimine.</span><span class="sxs-lookup"><span data-stu-id="9ae97-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="9ae97-112">Bir anahtar kasası ve gizli dağıtma</span><span class="sxs-lookup"><span data-stu-id="9ae97-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="9ae97-113">toocreate bir anahtar kasası ve gizli anahtarı, Azure CLI veya PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ae97-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="9ae97-114">Bu hello anahtar kasası şablon dağıtım için etkinleştirildiğinde dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9ae97-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="9ae97-115">Azure CLI için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ae97-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="9ae97-116">PowerShell için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ae97-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="9ae97-117">Erişim toohello gizli etkinleştir</span><span class="sxs-lookup"><span data-stu-id="9ae97-117">Enable access toohello secret</span></span>

<span data-ttu-id="9ae97-118">Yeni bir anahtar kasası veya varolan bir kullanıp kullanmadığınızı hello gizli hello şablon dağıtma bu hello kullanıcının erişebildiği emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae97-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="9ae97-119">Gizli başvuruda bulunan bir şablonu dağıtmayı hello kullanıcı hello olmalıdır `Microsoft.KeyVault/vaults/deploy/action` hello anahtar kasası için izni.</span><span class="sxs-lookup"><span data-stu-id="9ae97-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="9ae97-120">Merhaba [sahibi](../active-directory/role-based-access-built-in-roles.md#owner) ve [katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#contributor) rolleri hem bu erişimi verin.</span><span class="sxs-lookup"><span data-stu-id="9ae97-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="9ae97-121">Ayrıca bir [özel rol](../active-directory/role-based-access-control-custom-roles.md) , bu izni verir ve hello kullanıcı toothat rolünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae97-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="9ae97-122">Bir kullanıcı tooa rolü ekleme hakkında daha fazla bilgi için bkz: [tooadministrator rolleri Azure Active Directory'de bir kullanıcı atamak](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ae97-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="9ae97-123">Statik Kimliğine sahip bir gizlilik başvurusu</span><span class="sxs-lookup"><span data-stu-id="9ae97-123">Reference a secret with static ID</span></span>

<span data-ttu-id="9ae97-124">bir anahtar kasası gizli alan hello gibi herhangi bir şablonu şablonudur.</span><span class="sxs-lookup"><span data-stu-id="9ae97-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="9ae97-125">Çünkü **hello anahtar kasası hello parametre dosyasında değil hello şablon başvurusu.**</span><span class="sxs-lookup"><span data-stu-id="9ae97-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="9ae97-126">Örneğin, bir yönetici parolası içeren bir SQL veritabanı şablonu aşağıdaki hello dağıtır.</span><span class="sxs-lookup"><span data-stu-id="9ae97-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="9ae97-127">Merhaba parola parametresi tooa güvenli dize ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9ae97-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="9ae97-128">Ancak, bu değeri nereden geldiğini hello şablon belirtmiyor.</span><span class="sxs-lookup"><span data-stu-id="9ae97-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="9ae97-129">Şimdi, şablon önceki hello için bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ae97-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="9ae97-130">Merhaba parametre dosyasında hello şablon hello parametresinde hello adıyla eşleşen bir parametre belirtin.</span><span class="sxs-lookup"><span data-stu-id="9ae97-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="9ae97-131">Merhaba parametre değeri için hello hello anahtar Kasası'nı gizli başvuru.</span><span class="sxs-lookup"><span data-stu-id="9ae97-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="9ae97-132">Merhaba kaynak tanımlayıcısı hello anahtar kasasının ve hello gizli hello adını geçirerek hello gizli başvuru.</span><span class="sxs-lookup"><span data-stu-id="9ae97-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="9ae97-133">Merhaba, aşağıdaki örneğine hello anahtar kasasına gizli anahtarı zaten mevcut olmalıdır ve kendi kaynak kimliği için statik bir değer girin</span><span class="sxs-lookup"><span data-stu-id="9ae97-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="9ae97-134">Dinamik Kimliğine sahip bir gizlilik başvurusu</span><span class="sxs-lookup"><span data-stu-id="9ae97-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="9ae97-135">başlangıç anahtarı için bir statik kaynak kimliği toopass gizli nasıl kasa Hello önceki bölümde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9ae97-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="9ae97-136">Ancak, bazı senaryolarda tooreference hello geçerli dağıtımda göre değişen bir anahtar kasası gizli anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae97-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="9ae97-137">Bu durumda, sabit kodlu hello kaynak kimliği hello Parametreler dosyasında yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="9ae97-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="9ae97-138">Ne yazık ki, şablon ifadeleri hello parametreleri dosyada izin verilmez çünkü hello Parametreler dosyasında hello kaynak kimliği dinamik olarak oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="9ae97-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="9ae97-139">toodynamically hello kaynak kimliği için bir anahtar kasası gizli anahtar oluşturmak, iç içe geçmiş bir şablona hello gizli gereken hello kaynak taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae97-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="9ae97-140">Ana şablonunuzda hello iç içe geçmiş şablonuna ekleme ve dinamik olarak üretilen hello kaynak kimliği içeren bir parametre geçirin</span><span class="sxs-lookup"><span data-stu-id="9ae97-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9ae97-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ae97-141">Next steps</span></span>
* <span data-ttu-id="9ae97-142">Anahtar kasalarını hakkında genel bilgi için bkz: [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ae97-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="9ae97-143">Anahtar parolaları başvuran tüm örnekler için bkz: [anahtar kasası örnekler](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="9ae97-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

