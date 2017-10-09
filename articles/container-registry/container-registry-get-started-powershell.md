---
title: "aaaAzure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Nasıl toouse Azure kapsayıcı kayıt defteri depoları Docker görüntüleri"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Hello Azure PowerShell kullanarak özel bir Docker kapsayıcısı kayıt oluşturun
Komutlarda kullanmak [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate bir kapsayıcı kayıt defteri ve ayarlarını Windows bilgisayarınızdan yönetebilirsiniz. Ayrıca oluşturmak ve kapsayıcı kayıt defterleri hello kullanarak yönetmek [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), veya program aracılığıyla hello kapsayıcı kayıt defteri [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Arka plan ve kavramları için bkz: [hello genel bakış](container-registry-intro.md)
* Desteklenen cmdlet'leri tam bir listesi için bkz: [Azure kapsayıcı kayıt defteri yönetimi cmdlet'leri](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Ön koşullar
* **Azure PowerShell**: tooinstall ve Azure PowerShell ile çalışmaya başlama bkz hello [yükleme yönergeleri](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Çalıştırarak tooyour Azure aboneliği oturum `Login-AzureRMAccount`. Daha fazla bilgi için bkz: [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Kaynak grubu**: Kapsayıcı kayıt defteri oluşturmadan önce bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) oluşturun veya mevcut bir kaynak grubunu kullanın. Merhaba kaynak grubu hello kapsayıcı kayıt defteri hizmeti olduğu bir konumda olduğundan emin olun [kullanılabilir](https://azure.microsoft.com/regions/services/). toocreate Azure PowerShell kullanarak bir kaynak grubu bkz [PowerShell başvurusu hello](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Depolama hesabı** (isteğe bağlı): bir standart Azure oluşturma [depolama hesabı](../storage/common/storage-introduction.md) tooback hello kapsayıcı hello kayıt defterinde aynı konumu. Kayıt defteri ile oluştururken, bir depolama hesabı belirtmezseniz `New-AzureRMContainerRegistry`, hello komut sizin için bir tane oluşturur. bir depolama toocreate PowerShell kullanarak hesap için bkz: [PowerShell başvurusu hello](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Premium Depolama şu anda desteklenmemektedir.
* **Hizmet sorumlusu** (isteğe bağlı): bir kayıt defteri PowerShell ile oluşturduğunuzda, varsayılan olarak, erişim için kurulu değil. Gereksinimlerinize bağlı olarak, varolan bir Azure Active Directory hizmet asıl tooa kayıt atayın veya oluşturun ve yeni bir tane atayın. Alternatif olarak, hello kayıt defterindeki yönetici kullanıcı hesabı etkinleştirebilirsiniz. Bu makalenin sonraki bölümlerinde Hello bölümlere bakın. Kayıt defteri erişim hakkında daha fazla bilgi için bkz: [hello kapsayıcı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Kapsayıcı kayıt defteri oluşturma
Merhaba çalıştırmak `New-AzureRMContainerRegistry` komutu toocreate bir kapsayıcı kayıt defteri.

> [!TIP]
> Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın. Merhaba kayıt defteri adı hello örneklerde `MyRegistry`, ancak kendi benzersiz adı değiştirin.
>
>

kullandığı hello en az parametreleri toocreate kapsayıcı kayıt defteri komutu aşağıdaki hello `MyRegistry` hello kaynak grubunda `MyResourceGroup` hello Orta Güney ABD konum içinde:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` isteğe bağlıdır. Yoksa belirtilen hello kayıt defteri adını oluşan bir ada sahip bir depolama hesabı oluşturulur ve kaynak grubu bir zaman damgasına hello belirtilen.

## <a name="assign-a-service-principal"></a>Hizmet sorumlusu atama
PowerShell komutları tooassign bir Azure Active Directory kullanmak [hizmet sorumlusu](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa kayıt defteri. Merhaba hizmet sorumlusu Bu örneklerde hello sahibi rolü atanmış, ancak atayabilirsiniz [diğer rolleri](../active-directory/role-based-access-control-configure.md) istiyorsanız.

### <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma
Komutu aşağıdaki hello, yeni bir hizmet sorumlusu oluşturulur. Güçlü bir parola ile Merhaba belirtin `-Password` parametresi.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Yeni veya var olan hizmet sorumlusu atayın
Yeni veya varolan bir hizmet asıl tooa kayıt atayabilirsiniz. tooassign, örneğin aşağıdaki komut benzer toohello çalıştırmak sahibi rolü erişim toohello kayıt defteri,:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Oturum açma toohello kayıt defteri hello hizmet sorumlusu ile
Merhaba hizmet asıl toohello kayıt defteri atadıktan sonra komutu aşağıdaki hello kullanarak oturum açabilirsiniz:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Yönetici kimlik bilgilerini yönetme
Her kapsayıcı kayıt defteri için otomatik olarak bir yönetici hesabı oluşturulur ve varsayılan olarak devre dışı bırakılır. Merhaba aşağıdaki PowerShell komutlarını toomanage hello yönetici kimlik bilgilerini kapsayıcı kaydınız örnekler.

### <a name="obtain-admin-user-credentials"></a>Yönetici kullanıcı kimlik bilgileri edinme
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Mevcut bir kayıt defteri için yönetici kullanıcıyı etkinleştirme
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Mevcut bir kayıt defteri için yönetici kullanıcıyı devre dışı bırakma
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme](container-registry-get-started-docker-cli.md)
