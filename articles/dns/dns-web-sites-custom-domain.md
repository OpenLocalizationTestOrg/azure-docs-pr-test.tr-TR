---
title: "bir web uygulaması için özel DNS kayıtlarını aaaCreate | Microsoft Docs"
description: "Azure DNS kullanarak web uygulaması için toocreate özel etki alanı DNS kayıtları nasıl."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Özel bir etki alanındaki bir web uygulaması için DNS kayıtlarını oluşturun

Azure DNS toohost özel bir etki alanı, web uygulamaları için kullanabilirsiniz. Örneğin, bir Azure web uygulaması oluşturma ve kullanıcılara tooaccess istediğiniz ya da tarafından contoso.com ya da www.contoso.com bir FQDN kullanarak.

toodo bunu toocreate iki kayıtları içerir:

* Bir kök "A" kaydı işaret toocontoso.com
* Bir "CNAME" toohello işaret hello www adı için bir kayıt kaydedin.

Azure üzerinde bir web uygulaması için bir A kaydı oluşturursanız, bir kayıt, el ile güncelleştirilmelidir hello hello web uygulama değişikliklerini için temel alınan IP adresi hello aklınızda bulundurun.

## <a name="before-you-begin"></a>Başlamadan önce

Başlamadan önce öncelikle Azure DNS'de bir DNS bölgesi oluşturma ve hello bölgesi, kayıt tooAzure DNS temsilci.

1. toocreate bir DNS bölgesi içinde hello adımları izleyin [bir DNS bölgesi oluşturma](dns-getstarted-create-dnszone.md).
2. toodelegate, DNS, DNS tooAzure izleyin hello adımlarda [DNS etki alanı temsilcisi](dns-domain-delegation.md).

Bölge oluşturma ve tooAzure DNS temsilci sonra özel etki alanınız için daha sonra kayıt oluşturabilirsiniz.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Özel etki alanınız için bir A kaydı oluşturun

Bir A kaydı kullanılan toomap adı tooits IP adresi değil. Aşağıdaki örnek hello biz @ bir A kaydı tooan IPv4 adresi atanmaktadır:

### <a name="step-1"></a>1. Adım

Bir A kaydını oluşturun ve değişken $rs tooa atayın

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>2. Adım

Başlangıç IPv4 değeri daha önce oluşturduğunuz toohello kayıt kümesi Ekle "@" atanan hello $rs değişkenini kullanarak. Merhaba atanan IPv4 değerini web uygulamanız için başlangıç IP adresi olacaktır.

bir web uygulaması için toofind başlangıç IP adresi hello adımları izleyin [Azure App Service'te özel etki alanı adı yapılandırma](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>3. Adım

Merhaba değişiklikleri toohello kayıt kümesi uygulayın. Kullanım `Set-AzureRMDnsRecordSet` tooupload hello toohello kayıt kümesi tooAzure DNS değiştirir:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Özel etki alanınız için bir CNAME kaydı oluşturun

Etki alanınız zaten Azure DNS tarafından yönetiliyorsa (bkz [DNS etki alanı temsilcisi](dns-domain-delegation.md), hello örnek toocreate contoso.azurewebsites.net için bir CNAME kaydı aşağıdaki hello kullanabilirsiniz.

### <a name="step-1"></a>1. Adım

PowerShell'i açın ve yeni bir CNAME kaydı kümesi oluşturun ve değişken $rs tooa atayın. Bu örnekte, "" contoso.com"adlı bir süresi olan toolive" DNS bölgesinde 600 saniye kayıt kümesi türü CNAME oluşturur.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Aşağıdaki örnek hello hello yanıt ' dir.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>2. Adım

Merhaba CNAME kayıt kümesi oluşturulduktan sonra toohello web uygulaması işaret edecek bir diğer ad değeri toocreate gerekir.

Daha önce atanan değişkeni "$rs" Merhaba kullanarak hello web uygulama contoso.azurewebsites.net için hello toocreate hello diğer aşağıdaki PowerShell komutunu kullanabilirsiniz.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Aşağıdaki örnek hello hello yanıt ' dir.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>3. Adım

Hello kullanarak hello değişiklikleri `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Doğrulamak için hello kayıt oluşturulduğu doğru aşağıda gösterildiği gibi "nslookup kullanarak hello www.contoso.com" sorgulayarak:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Web uygulamaları için bir "awverify" kaydı oluşturun

Web uygulamanız için bir A kaydı toouse karar verirseniz, kendi hello özel etki alanı doğrulama işlemi tooensure gitmelidir. Bu doğrulama adımı "awverify" adlı özel bir CNAME kaydı oluşturarak yapılır. Bu bölüm, yalnızca tooA kayıtlar geçerlidir.

### <a name="step-1"></a>1. Adım

Merhaba "awverify" kaydı oluşturun. Merhaba aşağıdaki örnekte, contoso.com tooverify sahipliği hello özel etki alanı için hello "aweverify" kaydı oluşturacağız.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Aşağıdaki örnek hello hello yanıt ' dir.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>2. Adım

Merhaba kayıt kümesi "awverify" oluşturulduktan sonra diğer adı ayarlama hello CNAME kaydı atayın. Merhaba aşağıdaki örnekte, biz hello CNAMe kayıt kümesi diğer tooawverify.contoso.azurewebsites.net atar.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Aşağıdaki örnek hello hello yanıt ' dir.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>3. Adım

Hello kullanarak hello değişiklikleri `Set-AzureRMDnsRecordSet cmdlet`hello komutta aşağıda gösterildiği gibi.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba adımları [uygulama hizmeti için bir özel etki alanı adı yapılandırma](../app-service-web/web-sites-custom-domain-name.md) tooconfigure web uygulama toouse özel bir etki alanı.
