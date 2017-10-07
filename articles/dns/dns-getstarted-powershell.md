---
title: "aaaGet Azure PowerShell kullanarak DNS ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toocreate bir DNS bölgesi ve Azure DNS kaydında. Bu adım adım kılavuzu toocreate ve ilk DNS bölgenizi yönetmek ve PowerShell kullanarak kaydedin."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a>PowerShell ile Azure DNS’i kullanmaya başlama

> [!div class="op_single_selector"]
> * [Azure portal](dns-getstarted-portal.md)
> * [PowerShell](dns-getstarted-powershell.md)
> * [Azure CLI 1.0](dns-getstarted-cli-nodejs.md)
> * [Azure CLI 2.0](dns-getstarted-cli.md)

Bu makalede, ilk DNS bölgesi ve Azure PowerShell kullanarak kaydı hello adımları toocreate anlatılmaktadır. Ayrıca, hello Azure portal kullanarak aşağıdaki adımları gerçekleştirin veya platformlar arası Azure CLI hello.

Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir. Azure DNS, etki alanınızda barındırma toostart toocreate bir DNS bölgesi için o etki alanı adı gerekiyor. Ardından bu DNS bölgesinde etki alanınız için tüm DNS kayıtları oluşturulur. Son olarak, toopublish, DNS bölge toohello Internet tooconfigure hello ad sunucuları hello etki alanı için gerekir. Bu adımların her biri aşağıda açıklanmıştır.

Bu yönergeler, zaten yüklü ve tooAzure PowerShell imzalı varsayalım. Yardım için bkz. [PowerShell kullanarak nasıl toomanage DNS bölgeleri](dns-operations-dnszones.md).

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Merhaba DNS bölgesi oluşturmadan önce bir kaynak grubu toocontain hello DNS bölgesi oluşturulur. Merhaba aşağıdaki hello komut gösterir.

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

Bir DNS bölgesi hello kullanılarak oluşturulan `New-AzureRmDnsZone` cmdlet'i. Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*. Merhaba örnek toocreate bir DNS bölgesi Hello değerleri kendinizinkilerle değiştirerek kullanın.

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a>DNS kaydı oluşturma

Hello kullanarak kayıt kümeleri oluşturma `New-AzureRmDnsRecordSet` cmdlet'i. Merhaba aşağıdaki örnekte bir kayıt hello göreli adı "www" hello "contoso.com", "Contoso.com" kaynak grubunda DNS bölgesi içinde oluşturur. Merhaba tam hello kayıt kümesi "www.contoso.com" adıdır. Merhaba kayıt türü "A", "1.2.3.4" IP adresiyle, ve hello TTL 3600 saniyedir.

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

Diğer kayıt türleri için birden fazla kayıt ve toomodify mevcut kayıtları ile kayıt kümeleri için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini Azure PowerShell kullanarak](dns-operations-recordsets.md). 


## <a name="view-records"></a>Kayıtları görüntüleme

toolist hello DNS kayıtları, bölge içindeki kullanın:

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a>Ad sunucularını güncelleştirme

Sonra DNS bölgesi ve kayıtları doğru şekilde ayarlanan, tooconfigure gerek memnun, etki alanı adı toouse hello Azure DNS ad sunucuları. Bu DNS kayıtlarınızı hello Internet toofind üzerindeki diğer kullanıcılarla sağlar.

Merhaba bölgenizin ad sunucuları tarafından hello verilen `Get-AzureRmDnsZone` cmdlet:

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

Bu ad sunucuları hello etki alanı adı kayıt (Merhaba etki alanı adı satın aldığınız yerden) ile yapılandırılmalıdır. Şirketiniz hello seçeneği tooset hello ad sunucuları hello etki alanı için yukarı sunar. Daha fazla bilgi için bkz: [, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).

## <a name="delete-all-resources"></a>Tüm kaynakları silme

Bu makalede, adım aşağıdaki Al hello oluşturulan tüm kaynakları toodelete:

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Azure DNS hakkında daha fazla toolearn bkz [Azure DNS'ye genel bakış](dns-overview.md).

Azure DNS'de DNS bölgelerini yönetme hakkında daha fazla toolearn bkz [Azure PowerShell kullanarak DNS yönetme DNS bölgelerini](dns-operations-dnszones.md).

Azure DNS'de DNS kayıtlarını yönetme hakkında daha fazla toolearn bkz [yönetmek DNS kayıtlarını ve kayıt kümelerini PowerShell kullanarak Azure DNS'de](dns-operations-recordsets.md).

