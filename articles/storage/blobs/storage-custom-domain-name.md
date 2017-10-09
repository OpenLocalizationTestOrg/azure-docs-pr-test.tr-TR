---
title: "aaaConfigure Azure Blob storage uç noktanız için özel etki alanı adı | Microsoft Docs"
description: "Hello Azure portal toomap kendi kurallı ad (CNAME) toohello Blob storage uç bir Azure Storage hesabı kullanın."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: bfee6d28039f389ba2e2ed6b28d43894b6e15469
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Blob depolama uç noktası için özel etki alanı adınızı yapılandırma

Azure depolama hesabınızdaki blob verilerine erişmek için özel bir etki alanı yapılandırabilirsiniz. BLOB Depolama için varsayılan uç hello `<storage-account-name>.blob.core.windows.net`. Özel etki alanı ve alt etki alanı gibi eşlerseniz **www.contoso.com** toohello blob uç depolama hesabınız için kullanıcılarınız erişebilir sonra blob o etki alanını kullanan depolama hesabınızdaki veriler.

> [!IMPORTANT]
> Azure depolama henüz yerel olarak HTTPS ile özel etki alanlarını desteklemiyor. Şu anda yapabilecekleriniz [hello Azure CDN tooaccess BLOB'ları ile özel etki alanlarını HTTPS üzerinden kullanmak](storage-https-custom-domain-cdn.md).
>

Merhaba aşağıdaki tabloda gösterilmektedir adlı bir depolama hesabında bulunan blob veriler için birkaç örnek URL'leri **mystorageaccount**. Merhaba özel etki alanı kayıtlı hello depolama hesabı için **www.contoso.com**:

| Kaynak Türü | Varsayılan URL | Özel etki alanı URL'si |
| --- | --- | --- |
| Depolama hesabı | http://mystorageaccount.BLOB.Core.Windows.NET | http://www.contoso.com |
| Blob |http://mystorageaccount.BLOB.Core.Windows.NET/MyContainer/myblob | http://www.contoso.com/MyContainer/myblob |
| Kök kapsayıcı | http://mystorageaccount.BLOB.Core.Windows.NET/myblob veya http://mystorageaccount.blob.core.windows.net/$ kök/myblob| http://www.contoso.com/myblob ya da http://www.contoso.com/$ kök/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Doğrudan ara etki alanı eşleme karşılaştırması

Depolama hesabınız için özel etki alanı toohello blob uç noktanızı iki yolu toopoint vardır: eşleme ve hello kullanarak CNAME doğrudan *asverify* Ara alt etki alanı.

### <a name="direct-cname-mapping"></a>Doğrudan CNAME eşlemesi

Merhaba ilk ve en basit, toocreate toohello blob doğrudan uç noktası, özel etki alanı ve alt etki alanı eşleyen bir kurallı ad (CNAME) kaydı yöntemidir. Bir CNAME kaydı kaynak etki alanı tooa hedef etki eşleyen bir etki alanı adı sistemi (DNS) özelliğidir. Bu durumda, hello kaynak etki alanı kendi özel etki alanı ve alt etki alanı, örneğin olduğunda *www.contoso.com*. hello hedef etki alanıdır Blob Hizmeti uç noktanızı, örneğin  *mystorageaccount.BLOB.Core.Windows.NET*.

Merhaba doğrudan yöntemi kapsanan [özel bir etki alanı kayıt](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Ara eşlemesi ile *asverify*

Merhaba ikinci yöntem de CNAME kayıtları kullanır, ancak ilk Azure tooavoid kapalı kalma süresi tarafından tanınan özel bir alt etki alanı kullanır: **asverify**.

özel etki alanı tooa blob uç eşleme hello işlemi sonuçlanabilir hello etki alanı için kapalı kalma süresi kısa bir süre içinde hello kaydettirirken [Azure portal](https://portal.azure.com). Özel etki alanınızı şu anda bir uygulama sıfır kapalı kalma süresi gerektiren bir hizmet düzeyi sözleşmesi (SLA) ile destekleme sonra hello Azure kullanabilirsiniz *asverify* alt etki alanı Ara kayıt adımı olarak. Kullanıcıların bu ara adım sağlar hello DNS eşlemesi gerçekleştirilirken mümkün tooaccess etki alanınızda olan.

Merhaba Ara yöntemi kapsanan [hello kullanarak özel bir etki alanı kayıt *asverify* alt etki alanı](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Özel bir etki alanı kaydetme
Bu yordam tooregister kullanılamaz tooyour kullanıcılar olan hello etki alanınız hakkında hiçbir kaygılarınız varsa veya özel etki alanınızı uygulama şu anda barındırmayan özel etki alanınızı kullanacak.

Özel etki alanınızı şu anda kapalı kalma süresi olamaz uygulamanın destekleyen, özetlenen hello yordamı izleyin. [hello kullanarak özel bir etki alanı kayıt *asverify* alt etki alanı](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure bir özel etki alanı adı, DNS'de yeni bir CNAME kaydı oluşturmanız gerekir. Merhaba CNAME kaydı bir etki alanı adı için bir diğer ad belirtir. Bu durumda, depolama hesabınız için özel etki alanı toohello Blob storage uç noktanız hello adresini eşler.

Genellikle, etki alanı kayıt şirketinizin sitesinde etki alanınızın DNS ayarlarını yönetebilirsiniz. Her kayıt için bir CNAME kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, hello kavram aynı hello olduğu. Tooupgrade gerekebilir şekilde hello CNAME kaydı oluşturmadan önce bazı temel etki alanı kayıt paketler DNS yapılandırması, etki alanı kayıt paketiniz sunmaz.

1. Merhaba tooyour depolama hesabında gidin [Azure portal](https://portal.azure.com).
1. Altında **BLOB hizmeti** hello menü dikey penceresinde, seçin **özel etki alanı** tooopen hello *özel etki alanı* dikey.
1. Tooyour etki alanı kayıt şirketinizin sitesinde oturum ve DNS yönetme toohello sayfasına gidin. Bunu, **Etki Alanı Adı**, **DNS** veya **Ad Sunucusu Yönetimi** gibi bir bölümde bulabilirsiniz.
1. Merhaba bölümü CNAME'ler yönetmek için bulunamıyor. Merhaba sözcüklerinin olup olmadığına bakın ve toogo tooan Gelişmiş Ayarları sayfası olabilirsiniz **CNAME**, **diğer**, veya **alt etki alanları**.
1. Yeni bir CNAME kaydı oluşturun ve bir alt etki alanı diğer adı gibi sağlamak **www** veya **fotoğraf**. Ardından, Blob Hizmeti uç noktası hello biçimi olan bir ana bilgisayar adı sağlayın **mystorageaccount.blob.core.windows.net** (burada *mystorageaccount* depolama hesabınız hello adıdır). Merhaba ana bilgisayar adı toouse görünür öğe hello #1 *özel etki alanı* dikey penceresinde hello [Azure portal](https://portal.azure.com).
1. Merhaba hello metin kutusuna *özel etki alanı* dikey penceresinde hello [Azure portal](https://portal.azure.com), hello hello alt etki alanı dahil olmak üzere, özel etki alanı adını girin. Örneğin, etki alanınız varsa **contoso.com** ve alt etki alanı diğer adı **www**, girin **www.contoso.com**. Alt etki alanı ise **fotoğraf**, girin **photos.contoso.com**. hello alt etki alanı olan *gerekli*.
1. Seçin **kaydetmek** hello üzerinde *özel etki alanı* dikey tooregister özel etki alanınızı. Merhaba kayıt başarılı olursa, depolama hesabı başarıyla güncelleştirildi portal bir bildirim görürsünüz.

Yeni CNAME kaydı DNS dağıtıldıktan sonra kullanıcılarınızın özel etki alanınızı kullanarak hello uygun izinlere sahip oldukları sürece blob verilerini görüntüleyebilir.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Hello kullanarak özel bir etki alanı kayıt *asverify* alt etki alanı
Bu yordam tooregister kullanmak özel etki alanınızı özel etki alanınızı şu anda bir uygulama gerektiren bir SLA ile destekleniyorsa olması kapalı kalma süresi. Gelen işaret eden bir CNAME oluşturarak `asverify.<subdomain>.<customdomain>` çok`asverify.<storageaccount>.blob.core.windows.net`, etki alanınızı Azure ile önceden kaydedebilirsiniz. Ardından gelen işaret ikinci bir CNAME oluşturun `<subdomain>.<customdomain>` çok`<storageaccount>.blob.core.windows.net`, bu noktada yönlendirilmiş tooyour blob uç trafik tooyour özel etki alanı olacaktır.

Merhaba **asverify** alt etki alanı olan Azure tarafından tanınan özel bir alt etki alanı. Eklenmesini tarafından `asverify` tooyour kendi alt etki alanı, izin Azure toorecognize özel etki alanınızı hello hello etki alanı için DNS kaydı değiştirmeden. Merhaba hello etki alanı için DNS kaydı değiştirdiğinizde, kapalı kalma süresi olmadan eşlenen toohello blob uç olacaktır.

1. Merhaba tooyour depolama hesabında gidin [Azure portal](https://portal.azure.com).
1. Altında **BLOB hizmeti** hello menü dikey penceresinde, seçin **özel etki alanı** tooopen hello *özel etki alanı* dikey.
1. Tooyour DNS sağlayıcının Web sitesinde oturum ve DNS yönetme toohello sayfasına gidin. Bunu, **Etki Alanı Adı**, **DNS** veya **Ad Sunucusu Yönetimi** gibi bir bölümde bulabilirsiniz.
1. Merhaba bölümü CNAME'ler yönetmek için bulunamıyor. Merhaba sözcüklerinin olup olmadığına bakın ve toogo tooan Gelişmiş Ayarları sayfası olabilirsiniz **CNAME**, **diğer**, veya **alt etki alanları**.
1. Yeni bir CNAME kaydı oluşturun ve hello içeren bir alt etki alanı diğer adı sağlayın *asverify* alt etki alanı. Örneğin, **asverify.www** veya **asverify.photos**. Ardından, Blob Hizmeti uç noktası hello biçimi olan bir ana bilgisayar adı sağlayın **asverify.mystorageaccount.blob.core.windows.net** (burada **mystorageaccount** depolama hesabınız hello adıdır). Merhaba ana bilgisayar adı toouse görünür öğesi hello #2 *özel etki alanı* dikey penceresinde hello [Azure portal](https://portal.azure.com).
1. Merhaba hello metin kutusuna *özel etki alanı* dikey penceresinde hello [Azure portal](https://portal.azure.com), hello hello alt etki alanı dahil olmak üzere, özel etki alanı adını girin. İçermeyen *asverify*. Örneğin, etki alanınız varsa **contoso.com** ve alt etki alanı diğer adı **www**, girin **www.contoso.com**. Alt etki alanı ise **fotoğraf**, girin **photos.contoso.com**. hello alt etki alanı gereklidir.
1. Select hello **dolaylı CNAME doğrulaması kullan** onay kutusu.
1. Seçin **kaydetmek** hello üzerinde *özel etki alanı* dikey tooregister özel etki alanınızı. Merhaba kayıt başarılı olursa, depolama hesabı başarıyla güncelleştirildi belirten portal bir bildirim görürsünüz. Bu noktada, özel etki alanınızı Azure tarafından doğrulanıp doğrulanmadığını ancak trafik tooyour etki alanı değil henüz tooyour depolama hesabı yönlendiriliyor.
1. Tooyour DNS sağlayıcının Web sitesinde dönün ve alt etki alanı tooyour Blob Hizmeti uç noktası eşlemeleri başka bir CNAME kaydı oluşturun. Örneğin, hello alt etki alanı olarak belirtmeniz **www** veya **fotoğraf** (Merhaba olmadan *asverify*), ve ana bilgisayar adı olarak hello  **mystorageaccount.BLOB.Core.Windows.NET** (burada **mystorageaccount** depolama hesabınız hello adıdır). Bu adımda, özel etki alanınızı hello kaydı tamamlanır.
1. Son olarak, içeren hello oluşturduğunuz hello CNAME kaydı silebilirsiniz **asverify** şekliyle alt etki alanı bir ara adım olarak yalnızca gerekli.

Yeni CNAME kaydı DNS dağıtıldıktan sonra kullanıcılarınızın özel etki alanınızı kullanarak hello uygun izinlere sahip oldukları sürece blob verilerini görüntüleyebilir.

## <a name="test-your-custom-domain"></a>Özel etki alanınızı test

özel etki alanınız tooconfirm gerçekten tooyour Blob Hizmeti uç noktası eşlenen, açık bir kapsayıcıdaki depolama hesabınızda blob oluşturun. Ardından, bir web tarayıcısında biçimi tooaccess hello blob aşağıdaki hello bir URI kullanın:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Örneğin, aşağıdaki URI tooaccess hello web formunda hello kullanabilirsiniz **myforms** hello kapsayıcısında **photos.contoso.com** özel alt etki alanı:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Özel bir etki alanı kaydını

Blob storage uç noktanız için özel bir etki alanı tooderegister yordamları izleyerek hello birini kullanın.

### <a name="azure-portal"></a>Azure portalına

Hello Azure portal tooremove hello özel etki alanı ayarında Hello aşağıdakileri gerçekleştirin:

1. Merhaba tooyour depolama hesabında gidin [Azure portal](https://portal.azure.com).
1. Altında **BLOB hizmeti** hello menü dikey penceresinde, seçin **özel etki alanı** tooopen hello *özel etki alanı* dikey.
1. Özel etki alanı adınızı içeren hello metin kutusunun içeriğini Temizle hello.
1. Select hello **kaydetmek** düğmesi.

Merhaba özel etki alanı başarıyla kaldırıldı, depolama hesabı başarıyla güncelleştirildi belirten bir portal bildirim görürsünüz.

### <a name="azure-cli-20"></a>Azure CLI 2.0

Kullanım hello [az depolama hesabı güncelleştirme](https://docs.microsoft.com/cli/azure/storage/account#update) CLI komut ve boş bir dize belirtin (`""`) hello için `--custom-domain` bağımsız değişken değeri tooremove özel etki alanı kaydı.

* Komut biçimi:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Komut örneği:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Kullanım hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet'ini ve boş bir dize belirtin (`""`) hello için `-CustomDomainName` bağımsız değişken değeri tooremove özel etki alanı kaydı.

* Komut biçimi:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Komut örneği:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Sonraki adımlar
* [Bir özel etki alanı tooan Azure içerik teslim ağı (CDN) uç noktası eşleme](../../cdn/cdn-map-content-to-custom-domain.md)
* [HTTPS üzerinden özel etki alanları ile Hello Azure CDN tooaccess BLOB'ları kullanma](storage-https-custom-domain-cdn.md)
