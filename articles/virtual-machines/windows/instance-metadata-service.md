---
title: "Windows için örnek meta veri hizmeti aaaAzure | Microsoft Docs"
description: "Windows VM'ın işlem, ağ ve yaklaşan Bakımı olayları hakkında rESTful arabirimi tooget bilgi."
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a>Windows VM'ler için Azure örneği meta veri hizmeti


Hello Azure örneği meta veri hizmeti kullanılan toomanage ve sanal makineleri yapılandırma sanal makine örneği çalıştırma hakkında bilgi sağlar.
Bu, SKU, ağ yapılandırması ve yaklaşan Bakımı olayları gibi bilgileri içerir. Hangi tür bilgileri kullanılabilir daha fazla bilgi için bkz: [meta veri kategorileri](#instance-metadata-data-categories).

Azure'nın örnek meta verileri hizmetidir, erişilebilir tooall Iaas Vm'leri hello oluşturulan bir REST uç [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Merhaba uç nokta iyi bilinen yönlendirilemeyen IP adresinde mevcuttur (`169.254.169.254`), erişilebilir yalnızca VM hello içinde.



> [!IMPORTANT]
> Bu hizmet **genel olarak kullanılabilir** genel Azure bölgelerindeki. Genel Önizleme kamu, Çin ve Almanca Azure bulutu için ayarlanır. Düzenli olarak, sanal makine örnekleri hakkında güncelleştirmeleri tooexpose yeni bilgi alır. Bu sayfayı hello güncel yansıtır [veri kategorilerini](#instance-metadata-data-categories) kullanılabilir.



## <a name="service-availability"></a>Hizmet kullanılabilirliği
Merhaba hizmeti tüm genel olarak kullanılabilir genel Azure bölgelerde kullanılabilir. Merhaba hello kamu, Çin veya Almanya bölgelerde genel önizlemede hizmetidir.

Bölgeler                                        | Kullanılabilirlik?
-----------------------------------------------|-----------------------------------------------
[Tüm genel olarak kullanılabilir genel Azure bölgeleri](https://azure.microsoft.com/regions/)     | Genel olarak kullanılabilir 
[Azure Devlet Kurumları](https://azure.microsoft.com/overview/clouds/government/)              | Önizleme 
[Azure Çin](https://www.azure.cn/)                                                           | Önizleme
[Azure Almanya](https://azure.microsoft.com/overview/clouds/germany/)                    | Önizleme

Merhaba hizmet diğer Azure bulutta kullanılabilir olduğunda bu tabloya güncelleştirilir.

hello örneği meta veri hizmeti, çıkışı tootry oluşturma bir sanal makineden [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) veya hello [Azure portal](http://portal.azure.com) bölgeler ve izleme hello örneklere yukarıda hello içinde.

## <a name="usage"></a>Kullanım

### <a name="versioning"></a>Sürüm oluşturma
Merhaba örneği meta veri hizmeti sürümü tutulan ' dir. Sürümleri zorunludur ve hello geçerli sürümü `2017-04-02`.

> [!NOTE] 
> Önceki Önizleme sürümleri {son} hello api sürümü desteklenen zamanlanmış olaylar. Bu biçim artık desteklenmemektedir ve hello gelecekteki kullanım dışı kalacaktır.

Yeni sürümler eklediğimiz gibi komut dosyalarınızı belirli veri biçimleri üzerinde bağımlılıkları varsa, daha eski sürümlerini yine de uyumluluk için erişilebilir. Ancak, hello hizmeti genel olarak kullanılabilir olduğunda bu hello geçerli Önizleme version(2017-03-01) kullanılamayabilir unutmayın.

### <a name="using-headers"></a>Üst bilgileri kullanma
Merhaba örneği meta veri hizmeti sorguladığınızda hello üstbilgi sağlamalısınız `Metadata: true` tooensure hello talep istemeden yönlendirilmeyen.

### <a name="retrieving-metadata"></a>Meta veri alma

Örnek meta verileri oluşturulan yönetilen/kullanarak sanal makineleri çalıştırmak için kullanılabilir [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). İstek aşağıdaki hello kullanarak bir sanal makine örneği için tüm veri kategorilerini erişebilirsiniz:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Tüm örnek meta veri sorguları büyük/küçük harfe duyarlıdır.

### <a name="data-output"></a>Veri çıkışı
Varsayılan olarak, JSON biçiminde hello örneği meta veri hizmeti verileri döndürür (`Content-Type: application/json`). Ancak, farklı API'leri verileri farklı biçimlerde istediyseniz döndürebilir.
Merhaba aşağıdaki tabloda bir API destekleyebilir diğer veri biçimlerinin başvurudur.

API | Varsayılan veri biçimi | Diğer biçimlere
--------|---------------------|--------------
/instance | JSON | Metin
/scheduledevents | JSON | Yok

Varsayılan olmayan yanıt biçimi tooaccess hello isteği bir sorgu dizesi parametresi olarak hello istenen biçim belirtin. Örneğin:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Güvenlik
Merhaba örneği meta veri Hizmeti uç noktası yalnızca yönlendirilebilir olmayan bir IP adresi üzerinde sanal makine örneğini çalıştıran hello içinde erişilebilir. Ayrıca, herhangi bir ile istek bir `X-Forwarded-For` üstbilgi hello hizmeti tarafından reddedildi.
Biz de istekleri toocontain gerektiren bir `Metadata: true` gerçek isteği hello üstbilgi tooensure olan doğrudan istenen ve istenmeyen yeniden yönlendirme parçası değil. 

### <a name="error"></a>Hata
Bir veri öğesi bulunamadı veya hatalı biçimlendirilmiş bir istek varsa hello örneği meta veri hizmeti standart HTTP hatalarını döndürür. Örneğin:

HTTP durum kodu | Neden
----------------|-------
200 TAMAM |
400 Hatalı istek | Eksik `Metadata: true` üstbilgisi
404 Bulunamadı | Merhaba İstenen öğe does't var 
405 Yönteme izin verilmiyor | Yalnızca `GET` ve `POST` istekleri desteklenir
429 çok fazla istek | Merhaba API şu anda en fazla saniye başına 5 sorguları destekler
500 hizmet hatası     | Bir süre sonra yeniden deneyin

### <a name="examples"></a>Örnekler

> [!NOTE] 
> Tüm API yanıtları JSON dizelerdir. Okunabilirlik için pretty yazdırılan tüm aşağıdaki örnek yanıtlar.

#### <a name="retrieving-network-information"></a>Ağ bilgileri alınıyor

**İstek**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Yanıt**

> [!NOTE] 
> Merhaba yanıt bir JSON dizesidir. Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Genel IP adresi alınıyor

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Bir örneği için tüm meta veri alma

**İstek**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Yanıt**

> [!NOTE] 
> Merhaba yanıt bir JSON dizesidir. Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Windows sanal makinesinde meta verilerini alma

**İstek**

Örnek meta verileri alınabilir Windows hello PowerShell yardımcı programı `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Merhaba aracılığıyla veya `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Yanıt**

> [!NOTE] 
> Merhaba yanıt bir JSON dizesidir. Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Örnek meta veri kategorileri
Veri kategorilerini aşağıdaki hello hello örneği meta veri hizmeti kullanılabilir:

Veriler | Açıklama
-----|------------
location | Azure bölgesi hello VM çalışıyor
ad | Merhaba VM adı 
Teklif | Merhaba VM görüntüsü için bilgi sunar. Bu değer yalnızca Azure resmi Galerisi'nden dağıtılan görüntüleri için mevcuttur.
Yayımcı | Merhaba VM görüntüsü yayımcısı
SKU | Belirli SKU hello VM görüntüsü için  
Sürüm | Merhaba VM görüntüsü 
osType | Linux veya Windows 
platformUpdateDomain |  [Güncelleştirme etki alanı](manage-availability.md) hello VM çalışır
platformFaultDomain | [Hata etki alanı](manage-availability.md) hello VM çalışır
Bunun nedeni | [Benzersiz tanımlayıcı](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) hello VM için
vmSize | [VM boyutu](sizes.md)
IPv4/privateIpAddress | Merhaba VM yerel IPv4 adresi 
IPv4/Publicıpaddress | Merhaba VM genel IPv4 adresi
alt ağ/adresi | Merhaba VM alt ağ adresi
alt ağ/öneki | Alt ağ öneki, örnek 24
IPv6/IPADDRESS | Merhaba VM yerel IPv6 adresi
MacAddress | VM mac adresi 
scheduledevents | Genel önizlemesini görmek, şu anda [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Kullanım için örnek senaryolar  

### <a name="tracking-vm-running-on-azure"></a>Azure üzerinde çalışan VM izleme

Bir hizmet sağlayıcısı olarak tootrack hello yazılımınızı çalışan VM sayısı gerektirebilir veya hello VM tootrack benzersizliğini gereksinim aracılara sahip. toobe mümkün tooget benzersiz bir kimlik kullanmak hello bir VM için `vmId` örneği meta veri hizmetinden alan.

**İstek**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Yanıt**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Yerleştirme kapsayıcıların veri bölümlerini arıza/güncelleştirme etki alanı tabanlı 

Belirli senaryolar, farklı veri çoğaltmaları yerleşimini prime çok önemlidir. Örneğin, [HDFS çoğaltma yerleştirme](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) veya kapsayıcı yerleştirme aracılığıyla bir [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) tooknow hello gerektirebilir `platformFaultDomain` ve `platformUpdateDomain` VM üzerinde çalışan hello.
Bu verileri hello örneği meta veri hizmeti aracılığıyla doğrudan sorgulayabilir.

**İstek**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Yanıt**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Destek olayı sırasında hello VM hakkında daha fazla bilgi alma 

Bir hizmet sağlayıcısı olarak hello VM hakkında daha fazla bilgi bir destek çağrısı tooknow oluşturulacağı yeri alabilirsiniz. Merhaba müşteri tooshare soran hello işlem meta verileri VM hello tür hakkında temel bilgiler hello destek profesyonel tooknow için Azure üzerinde sağlayabilir. 

**İstek**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Yanıt**

> [!NOTE] 
> Merhaba yanıt bir JSON dizesidir. Aşağıdaki örnek yanıt hello okunabilirlik için pretty yazdırılmıştır.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Farklı diller hello VM içinde kullanarak meta veri hizmeti çağrılırken örnekleri 

Dil | Örnek 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.RB
LAN gidin   | https://github.com/Microsoft/azureimds/BLOB/master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.PY
C++      | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample-Windows.cpp
C#       | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.cs
Javascript | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/BLOB/master/IMDSSample.sh
    

## <a name="faq"></a>SSS
1. Merhaba hata alıyorum `400 Bad Request, Required metadata header not specified`. Bu ne anlama geliyor?
   * Hello örneği meta veri hizmeti gerektirir hello üstbilgi `Metadata: true` toobe hello istekte geçirildi. Bu üst hello REST çağrısı erişim toohello örneği meta veri hizmeti sağlar. 
2. Neden VM'im için işlem bilgi alıyorum değil mi?
   * Şu anda hello örneği meta veri hizmeti, yalnızca Azure Kaynak Yöneticisi ile oluşturulan örnekleri destekler. Hello gelecekteki, biz bulut hizmeti VM'ler için destek ekleyebilirsiniz.
3. Sanal Makinem Azure Resource Manager aracılığıyla geri bir süre oluşturdum. Bkz: değil neden ben meta veri bilgileri işlem?
   * Eylül 2016 sonra oluşturulan tüm VM'ler için ekleme bir [etiketi](../../azure-resource-manager/resource-group-using-tags.md) toostart görme işlem meta verileri. (Eylül 2016 öncesinde oluşturulan) eski VM'ler için ekleme/uzantıları veya veri diskleri toohello VM toorefresh meta verileri kaldır.
4. Neden iletisi alıyorum hello hata `500 Internal Server Error`?
   * Lütfen üstel geri alma sistem göre isteğinizi yeniden deneyin. Merhaba sorun devam ederse Azure desteğine başvurun.
5. Burada ek soruları/açıklamalar paylaşmak?
   * Yorumlarınızı üzerinde http://feedback.azure.com gönderin.
7. Bu sanal makine ölçek kümesi örneği için çalışır?
   * Evet meta veri hizmeti için ölçek kümesi örnek kullanılabilir. 
6. Merhaba hizmeti için destek nasıl sağlarım?
   * hello hizmet tooget desteği hello değil mümkün tooget meta veri yanıtı uzun denemeden sonra olduğunuz VM için Azure portalında bir destek sorununu oluşturma 

   ![Örnek meta verileri desteği](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Sonraki adımlar

- Merhaba hakkında daha fazla bilgi [zamanlanmış olayları](scheduled-events.md) API **genel önizlemede** hello örneği meta veri hizmeti tarafından sağlanan.
