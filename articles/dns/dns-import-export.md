---
title: "Dosya tooAzure Azure CLI 1.0 kullanarak DNS aaaImport ve dışarı aktarma bir etki alanı bölgesi | Microsoft Docs"
description: "Nasıl tooimport ve dışarı aktarma DNS dosya tooAzure DNS Azure CLI 1.0 kullanarak bölge öğrenin"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>İçeri ve hello Azure CLI 1.0 kullanarak bir DNS bölge dosyasına dışarı aktarma 

Bu makalede Azure DNS kullanarak tooimport ve dışarı aktarma DNS bölge dosyaları için Azure CLI 1.0 nasıl hello aracılığıyla anlatılmaktadır.

## <a name="introduction-toodns-zone-migration"></a>Giriş tooDNS bölge geçiş

Bir DNS bölge dosyasına hello bölgedeki her etki alanı adı sistemi (DNS) kaydı ayrıntılarını içeren bir metin dosyasıdır. DNS kayıtlarını DNS sistemler arasında aktarmak için uygun hale getirme standart bir biçimdedir. Bir bölge dosyası kullanarak bir hızlı, güvenilir ve uygun şekilde tootransfer içine veya dışına Azure DNS'ye bir DNS bölgesi değildir.

Azure DNS, içeri aktarma ve bölge dosyaları hello Azure komut satırı arabirimi (CLI) kullanarak dışa aktarma destekler. Bölge dosyası alma **değil** Azure PowerShell veya hello Azure portal aracılığıyla şu anda desteklenmiyor.

Hello Azure CLI 1.0 yönetme Azure Hizmetleri için kullanılan bir platformlar arası komut satırı aracıdır. Merhaba Windows, Mac ve Linux platformlarından hello kullanılabilir [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/). Platformlar arası desteği, en yaygın ad sunucusu yazılımı, alma ve bölge dosyaları, çünkü verme hello için önemlidir [BAĞLAMAK](https://www.isc.org/downloads/bind/), genellikle Linux üzerinde çalışır.

> [!NOTE]
> Şu anda hello Azure CLI iki sürümü de vardır. CLI1.0 Node.js üzerinde temel alır ve "azure" ile başlayan komutlar vardır.
> CLI2.0 Python üzerinde temel alır ve "az" ile başlayan komutlar vardır. Bölge dosyası alma her iki sürümde de destekleniyorsa hello CLI1.0 komutlarını kullanarak bu sayfasında açıklandığı şekilde öneririz.

## <a name="obtain-your-existing-dns-zone-file"></a>Var olan DNS bölge dosyanızı alın

Azure DNS'yi bir DNS bölge dosyasına içeri aktarmadan önce tooobtain hello bölge dosyasının bir kopyasını gerekir. Bu dosyanın kaynağına Hello hello DNS bölgesi şu anda barındırıldığı üzerinde bağlıdır.

* DNS bölgenizi (örneğin, etki alanı kayıt şirketi, ayrılmış DNS barındırma sağlayıcısı veya alternatif bulut sağlayıcısı) bir iş ortağı hizmeti tarafından barındırılıyorsa, bu hizmet hello özelliği toodownload hello DNS bölge dosyasına sağlamalıdır.
* DNS bölgenizi Windows DNS üzerinde barındırılıyorsa hello hello bölge dosyaları için varsayılan klasör olan **%systemroot%\system32\dns**. Merhaba tam yolu tooeach bölge dosyası ayrıca üzerinde hello gösterir **genel** hello DNS konsolunun sekmesi.
* DNS bölgesi, BIND kullanarak barındırılıyorsa hello bölge dosyası her bölge için hello konumunu hello BIND yapılandırma dosyasında belirtilen **named.conf**.

> [!NOTE]
> GoDaddy indirilen bölge dosyaları biraz standart olmayan bir biçime sahip. Azure DNS'yi bu bölge dosyalarını içeri aktarmadan önce toocorrect bu gerekir.
>
> Merhaba RDATA her DNS kaydının DNS adlarını tam olarak nitelenmiş adlar belirtilmiş, ancak bir sonlandırma yok "." Bu, göreli adları olarak diğer DNS sistemler tarafından yorumlanan anlamına gelir. Tooedit hello bölge dosyası tooappend hello sonlandırma gerekir "." Azure DNS'yi almadan önce tootheir adları.
>
> Örneğin, CNAME kaydı "www 3600 CNAME contoso.com ORMANINDAKİ" Merhaba çok değiştirilmelidir "www 3600 ın CNAME contoso.com."
> (bir sonlandırma ile ".").

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Azure DNS'yi bir DNS bölge dosyasına alın

Bir bölge dosyasını içeri bir zaten mevcut değilse yeni bir bölge, Azure DNS'de oluşturur. Merhaba bölgesi zaten varsa, hello hello bölge dosyası kayıt kümelerinde hello mevcut kayıt kümeleri birleştirilmesi gerekir.

### <a name="merge-behavior"></a>Davranış birleştirme

* Varsayılan olarak, var olan ve yeni kayıt kümelerini birleştirilir. Birleştirilmiş bir kayıt kümesi içinde aynı kayıtlar XML'deki yinelenen.
* Merhaba belirterek alternatif olarak, `--force` seçeneği, var olan kayıt kümeleri ile yeni kayıt kümeleri içeri aktarma işlemi değiştirir hello. Merhaba alınan bölge dosyasında ayarlanan karşılık gelen bir kayıt yok var olan kayıt kümeleri olması kaldırılmaz.
* Kayıt kümeleri birleştirildiğinde hello süresi toolive (TTL) önceden var olan kayıt kümelerinin kullanılır. Zaman `--force` olan kullanıldığında, hello hello yeni kayıt kümesi TTL kullanılır.
* Yetki (SOA) parametreleri başlangıcı (dışında `host`) hello alınan bölge dosyasından mi bağımsız olarak her zaman gerçekleştirilecek `--force` kullanılır. Benzer şekilde, ad sunucusu kaydı hello bölgenin tepesinde ayarlamak hello için hello TTL her zaman hello alınan bölge dosyasından alınır.
* İçeri aktarılan bir CNAME kaydı varolan bir CNAME değiştirmez kaydı ile aynı adı sürece hello hello `--force` parametresi.
* Bir çakışma bir CNAME kaydı ve başka bir kayıtla arasında duyduğunuzda (bakılmaksızın, varolan veya yeni) aynı ancak farklı ad hello türü, hello varolan kaydı korunur. Bu hello kullanımını bağımsızdır `--force`.

### <a name="additional-information-about-importing"></a>İçeri aktarma hakkında ek bilgi

Merhaba aşağıdaki notları hello bölge hakkında ek teknik ayrıntılar alma işlemi sağlar.

* Merhaba `$TTL` yönergesi isteğe bağlıdır ve desteklenmiyor. Durumlarda `$TTL` yönergesi verilen, açık bir TTL olmadan kayıtları alınır tooa varsayılan TTL 3600 saniyelik ayarlayın. İki kaydeder hello aynı kayıt kümesi belirtin farklı TTLs, hello daha düşük değer kullanılır.
* Merhaba `$ORIGIN` yönergesi isteğe bağlıdır ve desteklenmiyor. Durumlarda `$ORIGIN` ayarlandığında, hello varsayılan kullanılan hello bölge adı hello komut satırında belirtilen değerdir (Merhaba sonlandırma artı ".").
* Merhaba `$INCLUDE` ve `$GENERATE` yönergeleri desteklenmez.
* Bu kayıt türleri desteklenir: A, AAAA, CNAME, MX, NS, SOA, SRV ve TXT.
* bir bölge oluşturulduğunda SOA kaydına hello Azure DNS tarafından otomatik olarak oluşturulur. Bir bölge dosyasını içe aktardığınızda, tüm SOA parametreleri hello bölge dosyasından alınır *dışında* hello `host` parametresi. Bu parametre, Azure DNS tarafından sağlanan hello değeri kullanır. Bu parametre Azure DNS tarafından sağlanan toohello birincil ad sunucusu başvurmalıdır olmasıdır.
* Merhaba bölge oluşturulduğunda hello ad sunucusu kaydı hello bölgenin tepesinde ayarlamak da Azure DNS tarafından otomatik olarak oluşturulur. Yalnızca hello bu kayıt kümesi TTL alınır. Bu kayıtları Azure DNS tarafından sağlanan hello ad sunucusu adlarını içerir. Merhaba kayıt verilerini hello alınan bölge dosyasında yer alan hello değerlere göre yazılmaz.
* Genel Önizleme sırasında Azure DNS yalnızca tek dize TXT kaydı destekler. Çok dizeli TXT kayıtlarının birleştirilmiş ve kesilmiş too255 karakter olmalıdır.

### <a name="cli-format-and-values"></a>CLI biçim ve değerleri

hello Azure CLI komutu tooimport bir DNS bölgesi Hello biçimi şöyledir:

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Değerler:

* `<resource group>`Merhaba hello kaynak grubunun Azure DNS bölgesinde hello adıdır.
* `<zone name>`Merhaba bölge Hello adıdır.
* `<zone file name>`Merhaba yol/Merhaba bölge dosyası toobe içeri adıdır.

Bu ada sahip bir bölge hello kaynak grubunda mevcut değilse sizin için oluşturulur. Hello bölgesi zaten varsa, hello alınan kayıt kümelerini var olan kayıt kümeleri ile birleştirilir. toooverwrite hello mevcut kayıt kümelerini kullanma hello `--force` seçeneği.

Aslında, kullanım hello almadan olmadan bölge dosyasının tooverify hello biçimi `--parse-only` seçeneği.

### <a name="step-1-import-a-zone-file"></a>1. Adım Bir bölge dosyasını içeri aktarma

tooimport hello bölgeye ilişkin bölge dosyası **contoso.com**.

1. İçinde tooyour Azure aboneliği hello Azure CLI 1.0 kullanarak oturum açın.

    ```azurecli
    azure login
    ```

2. Merhaba aboneliği yeni DNS bölgenizi toocreate istediğiniz yeri seçin.

    ```azurecli
    azure account set <subscription name>
    ```

3. Hello Azure CLI anahtarlı tooResource Yöneticisi modunda olması gerekir böylece azure DNS bir Azure yalnızca Resource Manager, hizmetidir.

    ```azurecli
    azure config mode arm
    ```

4. Hello Azure DNS hizmeti kullanmadan önce abonelik toouse hello Microsoft.Network kaynak sağlayıcısı kaydetmeniz gerekir. (Her abonelik için tek seferlik bir işlem budur.)

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Zaten yoksa, ayrıca toocreate bir Resource Manager kaynak grubu gerekir.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. tooimport hello bölge **contoso.com** hello dosyasından **contoso.com.txt** hello kaynak grubunda yeni bir DNS bölgesi içinde **myresourcegroup**, hello komutu çalıştırın`azure network dns zone import`.<BR>Bu komut hello bölge dosyası yükler ve onu ayrıştırılamadı. Merhaba komutu hello Azure DNS hizmeti toocreate hello bölgesi üzerinde bir dizi komut yürütür ve tüm hello kayıt hello bölgesinde ayarlar. Merhaba komut penceresinde hello konsol, herhangi bir hata veya uyarı birlikte ilerlemeyi raporlar. Kayıt kümeleri serisinde oluşturulduğundan, birkaç dakika tooimport büyük bölge dosyası sürebilir.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>2. Adım Merhaba bölge doğrulayın

tooverify hello DNS bölgesi hello dosyasını aldıktan sonra yöntemler aşağıdaki hello herhangi birini kullanabilirsiniz:

* Azure CLI komutu aşağıdaki hello kullanarak hello kayıtları listeleyebilirsiniz:

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Merhaba PowerShell cmdlet'ini kullanarak hello kayıtları listeleyebilirsiniz `Get-AzureRmDnsRecordSet`.
* Kullanabileceğiniz `nslookup` tooverify ad çözümlemesi için hello kaydeder. Merhaba Bölge henüz temsilci değil çünkü toospecify hello doğru Azure DNS ad sunucuları açıkça gerekir. Merhaba aşağıdaki örnek tooretrieve hello ad sunucusu adlarını toohello bölge nasıl atanacağını gösterir. BT ayrıca nasıl kullanarak tooquery hello "www" kayıt gösterir `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>3. Adım DNS temsilcisini güncelleştir

Azure DNS ad sunucularının, doğruladıktan sonra hello bölge düzgün bir şekilde içeri tooupdate hello DNS temsilci toopoint toohello gerekir. Daha fazla bilgi için hello makalesine bakın [hello DNS temsilcisini Güncelleştir](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Azure DNS'yi bir DNS bölge dosyasına dışarı aktarma

hello Azure CLI komutu tooimport bir DNS bölgesi Hello biçimi şöyledir:

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Değerler:

* `<resource group>`Merhaba hello kaynak grubunun Azure DNS bölgesinde hello adıdır.
* `<zone name>`Merhaba bölge Hello adıdır.
* `<zone file name>`Merhaba yol/dışa aktarılan hello bölge dosyası toobe adıdır.

Merhaba bölge alma ile ilk olarak toosign gerektiği, aboneliğinizi seçin ve hello Azure CLI toouse Resource Manager modunu yapılandırın.

### <a name="tooexport-a-zone-file"></a>tooexport bölge dosyası

1. İçinde tooyour Azure aboneliği hello Azure CLI kullanarak oturum açın.

    ```azurecli
    azure login
    ```

2. DNS bölgenizi toocreate istediğiniz yere hello aboneliği seçin.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS bir Azure yalnızca Resource Manager hizmetidir. Hello Azure CLI anahtarlı tooResource Yöneticisi modunda olması gerekir.

    ```azurecli
    azure config mode arm
    ```

4. tooexport hello mevcut Azure DNS bölgesi **contoso.com** kaynak grubunda **myresourcegroup** toohello dosya **contoso.com.txt** (Merhaba geçerli klasörde), çalıştırın`azure network dns zone export`. Azure DNS hizmeti tooenumerate çağrıları hello bu komut hello bölgesinde kayıt kümeleri ve hello sonuçları tooa bağlama uyumlu bölge dosyası dışarı aktarma.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
