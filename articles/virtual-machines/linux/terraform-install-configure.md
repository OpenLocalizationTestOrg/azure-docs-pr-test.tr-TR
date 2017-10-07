---
title: "aaaInstall ve Azure'da Terraform tooprovision VM'ler ve diğer altyapıya yapılandırma | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Terraform toocreate Azure yapılandırma kaynakları"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: b6706f53b21347442def05a592c30a2d22718984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Yükleme ve Azure'da Terraform tooprovision VM'ler ve diğer altyapı yapılandırma 
Bu makalede hello gerekli adımları tooinstall ve Azure'da sanal makineleri gibi Terraform tooprovision kaynaklarını yapılandırın. Nasıl toocreate ve kullanım Azure kimlik bilgilerini tooenable Terraform tooprovision bulut kaynaklarını güvenli bir şekilde öğreneceksiniz.

HashiCorp Terraform kolay bir yolu toodefine sağlar ve bulut altyapısı HashiCorp yapılandırma dili (HCL) adlı bir özel şablon dili kullanarak dağıtın. Bu özel dil [kolay toowrite ve kolay toounderstand](terraform-create-complete-vm.md). Hello kullanarak ek olarak, `terraform plan` komutu, bunları yürütme önce hello değişiklikleri tooyour altyapı görsel öğe. Azure ile Terraform kullanarak bu adımları toostart izleyin.

## <a name="install-terraform"></a>Terraform yükleyin
tooinstall Terraform, [karşıdan](https://www.terraform.io/downloads.html) hello paket işletim sisteminize ayrı yükleme dizini için uygun. Merhaba indirme için genel bir yol da tanımlamanız gerekir bir tek bir yürütülebilir dosya içerir. Nasıl tooset hello Linux ve Mac yolda hakkında yönergeler için gidin çok[bu Web sayfası](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Nasıl tooset hello Windows yolda hakkında yönergeler için gidin çok[bu Web sayfası](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify hello çalıştırmak yüklemenizi `terraform` komutu. Çıkış olarak kullanılabilir Terraform seçeneklerin bir listesini görmelisiniz.

Ardından, tooallow Terraform erişim tooyour Azure aboneliği tooperform altyapı sağlanması gerekir.

## <a name="set-up-terraform-access-tooazure"></a>Terraform erişim tooAzure ayarlayın
tooenable Terraform tooprovision kaynakları Azure, Azure Active Directory'de (Azure AD) toocreate iki varlık gerekir: Azure AD uygulaması ve bir Azure AD hizmet sorumlusu. Ardından, Terraform komut dosyalarınızı bu varlıkları tanımlayıcılar kullanın. Bir hizmet sorumlusu genel Azure yerel örneğidir AD uygulaması. Bir hizmet sorumlusu ayrıntılı yerel erişim denetimi tooglobal kaynakları sağlar.

Azure AD uygulaması ve bir Azure AD hizmet sorumlusu birkaç yolu toocreate vardır. Merhaba kolay ve hızlı şekilde bugün toouse Azure CLI 2.0 olan hangi [indirin ve Windows, Linux veya Mac yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Ayrıca, PowerShell veya Azure CLI 1.0 toocreate hello gerekli güvenlik altyapısını kullanabilir. izleyen hello yönergeleri göstermek, nasıl tüm bu yaklaşım kullanarak Azure Terraform tooconfigure.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Azure CLI 2.0 (Windows, Linux veya Mac kullanıcıları için) kullanın 
Merhaba yükleyip sonra [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), komutu aşağıdaki hello vererek tooadminister içinde Azure aboneliğinizde oturum:

```
az login
```

>[!NOTE]
>Merhaba Çin'de, Azure Almanya veya Azure kamu Bulutlar kullanırsanız, toofirst gerekir, bulut ile hello Azure CLI toowork yapılandırın. Merhaba aşağıdakini çalıştırarak bunu yapabilirsiniz:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Birden çok Azure aboneliğiniz varsa, kendi ayrıntıları hello tarafından döndürülen `az login` komutu. Set hello `SUBSCRIPTION_ID` ortam değişkeni toohold hello hello değerini döndürdü `id` hello abonelikten alan toouse istiyor. 

Bu oturum için toouse istediğiniz hello abonelik ayarlayın.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

Merhaba hesap tooget hello abonelik kimliği sorgular ve Kiracı kimliği değerleri.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

Ardından, farklı kimlik bilgileri için Terraform oluşturun.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

AppID, parola, sp_name ve Kiracı döndürülür. Merhaba AppID ve parolayı not edin.

tooconfirm kimlik bilgilerinizi (hizmet sorumlusu) yeni bir Kabuğu'nu açın ve hello aşağıdaki komutları çalıştırın. Yedek hello sp_name, şifresi ve Kiracı için döndürülen:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>(Windows kullanıcıları için) PowerShell kullanma 
toouse bir Windows makinesine toowrite ve, Terraform yürütme komut dosyaları ve yapılandırma görevleri için PowerShell toouse hello sağ PowerShell araçları ile makinenizi yapılandırın. 

1. Merhaba adımları izleyerek PowerShell araçlarını yükleme [yükleyin ve Azure PowerShell yapılandırma](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. İndir ve Yürüt hello [azure setup.ps1 betik](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) hello PowerShell konsolundan.

3. toorun hello azure setup.ps1 komut dosyasını indirin ve hello yürütme `./azure-setup.ps1 setup` hello PowerShell konsolundan komutu. Daha sonra oturum açma tooyour yönetici ayrıcalıklarına sahip Azure aboneliği.

4. Bir uygulama adı (isteğe bağlı dize gerekli) sağlamanız istendiğinde. İsteğe bağlı olarak, istendiğinde güçlü bir parola sağlayın. Bir parola sağlamazsanız, güçlü bir parola sizin için .NET güvenlik kitaplıklarını kullanarak oluşturulur.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Azure CLI 1.0 (Linux veya Mac kullanıcıları için) kullanın
tooget Terraform ile Linux makineler veya Mac bilgisayarları yükleme hello uygun kitaplıkları makinenizde Azure CLI 1.0 ile başlatıldı.  

1. Hello adımları izleyerek Azure xPlat CLI araçlarını yükleme [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Karşıdan yükleyip JSON işlemci hello yönergeleri takip ederek [karşıdan jq](https://stedolan.github.io/jq/download/).

3. İndir ve Yürüt hello [azure setup.sh betik](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) hello konsol betikten bash.

4. toorun hello azure setup.sh komut dosyasını indirin ve hello yürütme `./azure-setup setup` hello konsolundan komutu. Daha sonra oturum açma tooyour yönetici ayrıcalıklarına sahip Azure aboneliği.
 
5. Bir uygulama adı (isteğe bağlı dize gerekli) sağlamanız istendiğinde. İsteğe bağlı olarak, istendiğinde güçlü bir parola sağlayın. Bir parola sağlamazsanız, güçlü bir parola sizin için .NET güvenlik kitaplıklarını kullanarak oluşturulur.

Tüm hello önceki betikler, bir Azure AD uygulaması ve hizmet sorumlusu oluşturun. Merhaba hizmet sorumlusu hello abonelikte katılımcı veya sahibi düzeyinde erişim alır. Merhaba yüksek sağladığı erişim düzeyi nedeniyle, bu komut dosyaları tarafından oluşturulan hello güvenlik bilgileri her zaman korumanız gerekir. Bu komut dosyaları tarafından sağlanan güvenlik bilgileri tüm dört adet Not: AppID, parola, ABONELİK_KİMLİĞİ ve tenant_id.

## <a name="set-environment-variables"></a>Ortam değişkenlerini ayarlama
Oluşturma ve Azure AD hizmet sorumlusu yapılandırdıktan sonra toolet gerek Terraform bilmeniz hello Kiracı kimliği, abonelik kimliği, istemci kimliği ve istemci gizli toouse. Bu değerleri Terraform komut dosyalarınızı gömerek açıklandığı gibi bunu yapabilirsiniz [Terraform kullanarak temel altyapı oluşturma](terraform-create-complete-vm.md). Alternatif olarak, ortam değişkenleri aşağıdaki hello ayarlayabilir (ve dolayısıyla yanlışlıkla etme veya kimlik bilgilerinizi paylaşımı kaçının):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Bu örnek Kabuk komut dosyası tooset bu değişkenleri kullanabilirsiniz:

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Azure Çin veya ya da Azure kamu içinde veya Azure Almanya ile Terraform kullanıyorsanız, ayrıca, tooset hello ortam değişkeni uygun şekilde gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Şimdi Terraform yükledikten ve Azure aboneliğinize altyapısı dağıtma başlayabilmeniz için Azure kimlik yapılandırılmış. Ardından, nasıl çok öğrenin[Terraform ile altyapı oluşturma](terraform-create-complete-vm.md).
