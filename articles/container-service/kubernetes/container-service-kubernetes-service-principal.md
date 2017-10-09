---
title: "Azure Kubernetes küme aaaService asıl | Microsoft Docs"
description: "Azure Container Service içindeki bir Kubernetes kümesi için Azure Active Directory hizmet sorumlusu oluşturma ve yönetme"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Container Service’te bir Kubernetes kümesi için Azure AD hizmet sorumlusu oluşturma


Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesi gerektiren bir [Azure Active Directory hizmet asıl](../../active-directory/develop/active-directory-application-objects.md) toointeract Azure API'leri ile. Merhaba hizmet sorumlusu gereklidir toodynamically yönetmek kaynakları gibi [kullanıcı tanımlı yollar](../../virtual-network/virtual-networks-udr-overview.md) ve hello [katman 4 Azure yük dengeleyici](../../load-balancer/load-balancer-overview.md). 


Bu makale bir hizmet yukarı farklı seçenekler tooset Kubernetes kümeniz için asıl gösterir. Örneğin, yüklü ve hello ayarlarsanız [Azure CLI 2.0](/cli/azure/install-az-cli2), hello çalıştırabilirsiniz [ `az acs create` ](/cli/azure/acs#create) komutu toocreate hello Kubernetes küme ve hello hizmeti hello asıl aynı anda.


## <a name="requirements-for-hello-service-principal"></a>Merhaba hizmet sorumlusu için gereksinimler

Karşılıyor gereksinimlerine hello veya yeni bir tane oluşturun var olan bir Azure AD hizmet sorumlusu kullanabilirsiniz.

* **Kapsam**: hello abonelik hello kaynak grubunda kullanılan toodeploy hello Kubernetes küme veya hello abonelik toodeploy hello küme (daha az giderilirken) kullanılır.

* **Rol**: **Katkıda bulunan**

* **Gizli anahtar**: Bir parola olmalıdır. Şu anda sertifika kimlik doğrulaması için ayarlanmış bir hizmet sorumlusunu kullanamazsınız.

> [!IMPORTANT] 
> bir hizmet sorumlusu toocreate, aboneliğinizde Azure AD kiracısı ve tooassign hello uygulama tooa rolüne sahip bir uygulama izinleri tooregister olmalıdır. Merhaba gerekli izinlere sahip toosee [hello Portal denetleyin](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>1. Seçenek: Azure AD'de hizmet sorumlusu oluşturma

Kubernetes kümenizi dağıtmadan önce bir Azure AD hizmet sorumlusu toocreate istiyorsanız, Azure çeşitli yöntemler sağlar. 

Aşağıdaki örnek komutlar hello Göster, nasıl toodo bu hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). Alternatif olarak kullanarak bir hizmet asıl oluşturabilirsiniz [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), veya diğer yöntemleri.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

Çıktı (burada Redaksiyonu yapılmış gösterilen) benzer toohello aşağıda verilmiştir:

![Hizmet sorumlusu oluşturma](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Vurgulanan hello olan **istemci kimliği** (`appId`) ve hello **gizli** (`password`), Küme dağıtımı için hizmet asıl parametreleri olarak kullanma.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Hizmet sorumlusu hello Kubernetes küme oluştururken belirtin

Merhaba sağlamak **istemci kimliği** (hello olarak da bilinir `appId`, uygulama kimliği için) ve **gizli** (`password`) var olan bir hizmet olarak hello oluşturduğunuzda parametreler sorumlusu Kubernetes küme. Bu makalede başlayan hello hello gereksinimlerine Hello hizmet sorumlusu karşıladığından emin olun.

Hello kullanarak hello Kubernetes kümesini dağıtırken bu parametreleri belirtebilirsiniz [Azure komut satırı arabirimi (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), veya diğer yöntemleri.

>[!TIP] 
>Merhaba belirtirken **istemci kimliği**, emin toouse hello olması `appId`, değil hello `ObjectId`, hello hizmet asıl.
>

Merhaba aşağıdaki örnek bir yolu toopass hello Azure CLI 2.0 hello parametrelerle gösterir. Bu örnek hello kullanır [Kubernetes hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Karşıdan](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello şablon parametreleri dosyası `azuredeploy.parameters.json` github'dan.

2. toospecify hello hizmet sorumlusu için değerleri girin `servicePrincipalClientId` ve `servicePrincipalClientSecret` hello dosyasında. (Ayrıca tooprovide için kendi değerlerinizi ihtiyacınız `dnsNamePrefix` ve `sshRSAPublicKey`. Merhaba ikinci hello SSH ortak anahtarı tooaccess hello kümedir.) Merhaba dosyasını kaydedin.

    ![Hizmet sorumlusu parametrelerini iletme](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Aşağıdaki komut, kullanarak çalışma hello `--parameters` tooset hello yol toohello azuredeploy.parameters.json dosyası. Bu komut hello küme çağrılan oluşturduğunuz bir kaynak grubunda dağıtır `myResourceGroup` hello Batı ABD bölgesindeki.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Seçeneği 2: Merhaba küme oluştururken, bir hizmet sorumlusu oluşturma`az acs create`

Merhaba çalıştırırsanız [ `az acs create` ](/cli/azure/acs#create) komutu toocreate Kubernetes küme Merhaba, hello seçeneği toogenerate bir hizmet sorumlusu otomatik olarak olur.

Diğer Kubernetes kümesi oluşturma seçeneklerinde olduğu gibi, `az acs create` çalıştırırken mevcut bir hizmet sorumlusunun parametrelerini belirtebilirsiniz. Ancak, bu parametreyi de atladığınızda hello Azure CLI otomatik olarak kullanmak için bir tane kapsayıcı hizmeti ile oluşturur. Bu saydam hello dağıtımı sırasında gerçekleşir. 

Merhaba aşağıdaki komutu Kubernetes küme oluşturur ve SSH anahtarları ve hizmet asıl kimlik bilgilerini oluşturur:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Hesabınızı hello Azure AD ve abonelik izinleri toocreate yoksa ve bir hizmet sorumlusu hello komutu benzer bir hata çok oluşturur`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Diğer konular

* Bir hizmet asıl izinleri toocreate aboneliğinizde sahip değilseniz, tooask gerekebilecek Azure AD veya abonelik Yöneticisi tooassign hello gerekli izinleri ya da Azure kapsayıcı hizmeti ile bir hizmet asıl toouse için isteyin. 

* Merhaba hizmet sorumlusu Kubernetes için hello küme yapılandırmasının bir parçasıdır. Ancak, hello kimlik toodeploy hello küme kullanmayın.

* Her hizmet sorumlusunun bir Azure AD uygulamasıyla ilişkilendirilmiş olması gerekir. Merhaba hizmet sorumlusu Kubernetes kümesi için geçerli tüm Azure ile ilişkilendirilebilir AD uygulama adı (örneğin: `https://www.contoso.org/example`). Merhaba uygulaması Hello URL'sini toobe gerçek bir uç nokta yok.

* Merhaba hizmet sorumlusu belirlerken **istemci kimliği**, hello hello değerini kullanabilirsiniz `appId` (Bu makalede gösterildiği gibi) veya hello karşılık gelen hizmet sorumlusu `name` (örneğin,`https://www.contoso.org/example`).

* Hello Yöneticisi ve hello Kubernetes kümedeki sanal makineleri aracı üzerinde hello hizmet asıl kimlik hello dosya /etc/kubernetes/azure.json depolanır.

* Merhaba kullandığınızda `az acs create` toogenerate hello hizmet sorumlusu komutu otomatik olarak, hello hizmet asıl kimlik toohello dosya ~/.azure/acsServicePrincipal.json hello makinede kullanılan toorun hello komutu yazılır. 

* Merhaba kullandığınızda `az acs create` toogenerate hello hizmet sorumlusu komutu otomatik olarak, hello hizmet sorumlusu kimliğini de bir [Azure kapsayıcı kayıt defteri](../../container-registry/container-registry-intro.md) hello aynı oluşturulan abonelik.




## <a name="next-steps"></a>Sonraki adımlar

* Kapsayıcı hizmeti kümenizde [Kubernetes ile çalışmaya başlama](container-service-kubernetes-walkthrough.md).

* tootroubleshoot hello hizmet sorumlusu Kubernetes için bkz: Merhaba [ACS altyapısı belgelerine](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


