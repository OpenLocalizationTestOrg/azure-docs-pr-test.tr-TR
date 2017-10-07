---
title: "Azure Hizmetleri için DNS aaaReverse | Microsoft Docs"
description: "Nasıl tooconfigure ters DNS araması Azure içinde barındırılan hizmetler için bilgi edinin"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Azure üzerinde barındırılan hizmetleri için ters DNS yapılandırma

Bu makalede nasıl tooconfigure ters DNS araması Azure içinde barındırılan hizmetler için açıklanmaktadır.

Azure Hizmetleri Azure tarafından atanan ve Microsoft tarafından ait IP adresleri kullanın. Geriye doğru DNS kayıtlarının (PTR kayıtları) hello karşılık gelen Microsoft ait geriye doğru DNS araması bölgelerinde oluşturulması gerekir. Bu makalede açıklanır nasıl toodo bu.

Bu senaryo hello yeteneği çok karıştırılmamalıdır[hello geriye doğru DNS arama bölgeleri Azure DNS'de, atanan IP aralıkları için ana bilgisayar](dns-reverse-dns-hosting.md). Bu durumda, hello geriye doğru arama bölgesi tarafından temsil edilen hello IP aralıkları tooyour kuruluş, genellikle ISS'niz tarafından atanmış olması gerekir.

Bu makalede okumadan önce bu bilgi sahibi olmanız [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).

Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).
* Merhaba Resource Manager dağıtım modelinde, işlem kaynakları (örneğin, sanal makineler, sanal makine ölçek kümeleri veya Service Fabric kümeleri) Publicıpaddress kaynak sunulur. Geriye doğru DNS araması hello Publicıpaddress hello 'ReverseFqdn' özelliği kullanılarak yapılandırılır.
* Merhaba Klasik dağıtım modelinde, bulut hizmetlerini kullanarak işlem kaynaklarını sunulur. Geriye doğru DNS araması hello bulut hizmeti hello 'ReverseDnsFqdn' özelliği kullanılarak yapılandırılır.

Geriye doğru DNS hello Azure uygulama hizmeti şu anda desteklenmiyor.

## <a name="validation-of-reverse-dns-records"></a>Geriye doğru DNS kayıtlarını doğrulama

Bir üçüncü taraf mümkün toocreate geriye doğru DNS kayıtlarını Azure hizmeti eşleme tooyour DNS etki alanları için olmamalıdır. tooprevent Bu, Azure yalnızca aynı hello veya DNS adı veya IP adresini Publicıpaddress veya Bulut hello için çözümler hizmet hello aynı hello geriye doğru DNS kaydında belirtilen etki alanı adı olduğu geriye doğru DNS kaydı hello oluşturulmasını sağlayan Azure aboneliği.

Bu doğrulama Hello geriye doğru DNS kaydı kümesi değiştirildiğinde veya yalnızca gerçekleştirilir. Düzenli aralıklarla yeniden doğrulama yapılmaz.

Örneğin: Merhaba Publicıpaddress kaynak hello DNS adı contosoapp1.northus.cloudapp.azure.com ve IP adresi 23.96.52.53 sahip olduğunu varsayın. Merhaba ReverseFqdn Publicıpaddress olarak belirtilen hello:
* Merhaba Publicıpaddress Hello DNS adı, contosoapp1.northus.cloudapp.azure.com
* Merhaba DNS hello içinde farklı bir Publicıpaddress için aynı adı contosoapp2.westus.cloudapp.azure.com gibi abonelik
* Bu ad olduğu sürece bir gösterim DNS, app1.contoso.com gibi ad *ilk* bir CNAME toocontosoapp1.northus.cloudapp.azure.com veya tooa olarak farklı Publicıpaddress hello yapılandırılmış aynı abonelik.
* Bu ad olduğu sürece bir gösterim DNS, app1.contoso.com gibi ad *ilk* hello 23.96.52.53 veya farklı bir Publicıpaddress toohello IP adresini bir A kaydı toohello IP adresi yapılandırılmış aynı abonelik.

Merhaba aynı kısıtlamaları tooreverse DNS bulut Hizmetleri için geçerlidir.


## <a name="reverse-dns-for-publicipaddress-resources"></a>Geriye doğru DNS Publicıpaddress kaynaklar için

Bu bölümde nasıl tooconfigure ters DNS hello Resource Manager dağıtım modelinde, Azure PowerShell, Azure CLI 1.0 veya Azure CLI 2.0 kullanarak Publicıpaddress kaynaklar için ayrıntılı yönergeler sağlar. Geriye doğru DNS Publicıpaddress kaynakları için yapılandırma hello Azure portal şu anda desteklenmiyor.

Azure şu anda destekler DNS yalnızca IPv4 Publicıpaddress kaynaklar için ters çevrilir. IPv6 için desteklenmiyor.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Geriye doğru DNS tooan Publicıpaddresses varolan Ekle

#### <a name="powershell"></a>PowerShell

Publicıpaddress varolan tooadd geriye doğru DNS tooan:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd ters DNS tooan zaten bir DNS adı yok Publicıpaddress var, bir DNS adı belirtmeniz gerekir:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

Publicıpaddress varolan tooadd geriye doğru DNS tooan:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd ters DNS tooan zaten bir DNS adı yok Publicıpaddress var, bir DNS adı belirtmeniz gerekir:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

Publicıpaddress varolan tooadd geriye doğru DNS tooan:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd ters DNS tooan zaten bir DNS adı yok Publicıpaddress var, bir DNS adı belirtmeniz gerekir:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Geriye doğru DNS ile bir ortak IP adresi oluştur

toocreate zaten belirtilen hello ters DNS özelliği ile yeni bir Publicıpaddress:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Varolan bir Publicıpaddress için ters DNS görünümü

tooview hello değer var olan bir Publicıpaddress için yapılandırılmış:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Mevcut ortak IP adreslerinden geriye doğru DNS Kaldır

Varolan bir Publicıpaddress geriye doğru DNS özelliğinden tooremove:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Bulut Hizmetleri için ters DNS yapılandırma

Bu bölümde nasıl tooconfigure ters DNS için bulut hizmetlerini Azure PowerShell kullanarak hello Klasik dağıtım modelinde, ayrıntılı yönergeler sağlar. Bulut Hizmetleri için ters DNS yapılandırma hello Azure portal, Azure CLI 1.0 veya Azure CLI 2.0 desteklenmiyor.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Geriye doğru DNS tooexisting bulut Hizmetleri Ekle

Bulut hizmeti varolan geriye doğru DNS kaydı tooan tooadd:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Geriye doğru DNS ile bir bulut hizmeti oluştur

toocreate zaten belirtilen hello ters DNS özelliği ile yeni bir bulut hizmeti:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Mevcut bulut Hizmetleri için ters DNS görünümü

tooview hello ters DNS özelliği var olan bir bulut hizmeti için:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Mevcut bulut hizmetlerinden geriye doğru DNS Kaldır

var olan bir bulut hizmetinden geriye doğru DNS özelliği tooremove:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>SSS

### <a name="how-much-do-reverse-dns-records-cost"></a>DNS kayıtları maliyeti ne kadar ters?

Bunlar boş!  Geriye doğru DNS kayıtlarını veya sorguları için ek bir maliyet yoktur.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>My geriye doğru DNS kayıtları çözümleme Internet hello?

Evet. Azure hizmetiniz için hello ters DNS özelliği ayarladıktan sonra tüm hello DNS temsilcilerine Azure yönetir ve tüm Internet kullanıcılar için DNS kaydı ters tooensure çözümler DNS bölgeleri gerekli.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Varsayılan geriye doğru DNS kayıtları için Azure Hizmetlerim oluşturulur?

Hayır. Geriye doğru DNS, bir katılımı özelliğidir. Geriye doğru DNS kayıtlarını değil tooconfigure seçerseniz oluşturulan varsayılan bunları.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Merhaba biçimi hello tam etki alanı adı (FQDN) nedir?

FQDN'ler ileriye doğru sırada belirtilir ve bir nokta (örneğin, "app1.contoso.com.") ile bitmelidir.

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Hello için hello doğrulama denetimi belirtmiş olduğunuz DNS geriye doğru başarısız olur ne olur?

Merhaba geriye doğru DNS doğrulama denetimi başarısız olduğunda, hello işlemi tooconfigure hello geriye doğru DNS kaydı başarısız olur. Merhaba geriye doğru DNS değeri gerektiği gibi düzeltin ve yeniden deneyin.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Azure App Service için ters DNS yapılandırabilir miyim?

Hayır. Geriye doğru DNS hello Azure App Service için desteklenmiyor.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Birden çok geriye doğru DNS kaydı için Azure Hizmetim yapılandırabilir miyim?

Hayır. Azure, her Azure bulut hizmeti veya Publicıpaddress için tek bir geriye doğru DNS kaydını destekler.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>IPv6 Publicıpaddress kaynaklar için ters DNS yapılandırabilir miyim?

Hayır. Azure şu anda destekler DNS yalnızca IPv4 Publicıpaddress kaynaklar ve bulut Hizmetleri için ters çevrilir.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Azure işlem Hizmetlerim e-postaları tooexternal etki alanları gönderebilirim?

Hayır. [Azure işlem Hizmetleri gönderen e-postaları tooexternal etki alanlarını desteklemiyor](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Sonraki adımlar

Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Nasıl çok öğrenin[konak hello geriye doğru arama bölgesi ISS atanan IP aralığınızı Azure DNS'de için](dns-reverse-dns-for-azure-services.md).

