---
title: aaaDeploy OpenShift kaynak tooAzure | Microsoft Docs
description: "Toodeploy OpenShift kaynak tooAzure sanal makineler hakkında bilgi edinin."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>OpenShift kaynak tooAzure sanal makineleri dağıtma 

[OpenShift kaynak](https://www.openshift.org/) üzerinde oluşturulan bir açık kaynak kapsayıcı platformdur [Kubernetes](https://kubernetes.io/). Dağıtma, ölçeklendirme ve çok kiracılı uygulamalara işletim hello sürecini basitleştirir. 

Bu kılavuz, Azure sanal makineleri kullanma OpenShift kaynak toodeploy nasıl hello Azure CLI ve Azure Resource Manager şablonları açıklar. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * KeyVault toomanage hello OpenShift kümesi için SSH anahtarları oluşturma.
> * Azure VM'ler OpenShift kümede dağıtın. 
> * Yükleme ve yapılandırma hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello küme.
> * Merhaba OpenShift dağıtım özelleştirin.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

Bu hızlı başlangıç hello Azure CLI Sürüm 2.0.8 gerektirir veya sonraki bir sürümü. çalıştırma toofind hello sürüm `az --version`. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum 
Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin veya **deneyin** toouse bulut Kabuk.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Anahtar kasası oluşturma
KeyVault toostore hello ile Merhaba hello kümesi için SSH anahtarları oluşturma [az keyvault oluşturma](/cli/azure/keyvault#create) komutu.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>SSH anahtarı oluşturma 
Bir SSH anahtarı gerekli toosecure erişim toohello OpenShift kaynak kümesi olur. Bir SSH anahtarı çifti oluşturma hello kullanarak `ssh-keygen` komutu. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Merhaba SSH anahtar çifti oluşturduğunuz bir parola olmaması gerekir.

Windows, SSH anahtarları hakkında daha fazla bilgi için [nasıl Windows toocreate SSH anahtarları](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Anahtar kasasına SSH özel anahtar depolama
Merhaba OpenShift dağıtım toohello OpenShift ana toosecure erişim oluşturulan hello SSH anahtarı kullanır. tooenable hello dağıtım toosecurely hello SSH anahtarı almak, komutu aşağıdaki hello kullanarak anahtar kasasına hello anahtarını depolamak.

# <a name="enabled-for-template-deployment"></a>Şablon dağıtımı için etkin
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma 
OpenShift bir kullanıcı adı ve parola veya bir hizmet sorumlusu kullanarak Azure ile iletişim kurar. Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve OpenShift gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir. Denetim ve toowhat işlemleri hello hizmet sorumlusu Azure'da gerçekleştirebilirsiniz gibi hello izinleri tanımlayın. yalnızca bir kullanıcı adı ve parola sağlayarak tooimprove güvenliği, bu örnek temel bir hizmet sorumlusu oluşturur.

Bir hizmet sorumlusu ile oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) ve OpenShift gereken çıktı hello kimlik bilgileri:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Merhaba komutundan geri döndürülen hello AppID özelliği not edin.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Güvenli olmayan bir parola oluşturmayın.  [Azure AD parola kuralları ve kısıtlamaları](/azure/active-directory/active-directory-passwords-policy) yönergelerini izleyin.

Hizmet sorumluları hakkında daha fazla bilgi için bkz: [bir Azure hizmet sorumlusu Azure CLI 2.0 ile oluşturun.](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Merhaba OpenShift kaynak şablonu dağıtma
Sonraki OpenShift bir Azure Resource Manager şablonu kullanarak kaynak dağıtın. 

> [!NOTE] 
> Merhaba aşağıdaki komutu gerektirir az CLI 2.0.8 veya sonraki bir sürümü. Doğrulayabilirsiniz az CLI hello hello sürümüyle `az --version` komutu. tooupdate hello CLI Sürüm bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).

Kullanım hello `appId` daha önce oluşturduğunuz Merhaba hello hizmet sorumlusu değerinden `aadClientId` parametresi.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
Merhaba dağıtım too20 dakika toocomplete sürebilir. Merhaba dağıtım tamamlandığında hello hello OpenShift konsol URL'sini ve hello DNS adını yöneticisidir OpenShift toohello terminal yazdırılmıştır.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Toohello OpenShift kümesine bağlanın
Merhaba dağıtım tamamlandığında hello kullanarak hello tarayıcı kullanarak toohello OpenShift konsol bağlantısı `OpenShift Console Uri`. Alternatif olarak, komutu aşağıdaki hello kullanarak toohello OpenShift asıl bağlanabilir.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Kaynakları temizleme
Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, OpenShift küme ve tüm ilişkili kaynakları komutu.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu öğretici, öğrenilmiş nasıl için:
> [!div class="checklist"]
> * KeyVault toomanage hello OpenShift kümesi için SSH anahtarları oluşturma.
> * Azure VM'ler OpenShift kümede dağıtın. 
> * Yükleme ve yapılandırma hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello küme.

Şimdi bu OpenShift kaynak küme dağıtılır. OpenShift öğreticileri toolearn nasıl izleyebilirsiniz toodeploy ilk uygulama ve kullanım OpenShift araçları hello. Bkz: [OpenShift kaynağı ile çalışmaya başlama](https://docs.openshift.org/latest/getting_started/index.html) tooget başlatıldı. 
