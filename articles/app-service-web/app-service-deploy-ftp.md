---
title: aaaDeploy, uygulama tooAzure uygulama FTP/S kullanarak hizmeti | Microsoft Docs
description: "Bilgi nasıl toodeploy uygulama hizmetini kullanarak FTP veya FTPS, uygulama tooAzure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Uygulama tooAzure uygulama FTP/S kullanarak hizmeti dağıtma

Bu makale size nasıl gösterir toouse FTP veya web uygulaması, mobil uygulama arka ucu veya API uygulaması toodeploy çok FTPS[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Uygulamanız için Hello FTP/S uç nokta zaten etkindir. Herhangi bir yapılandırma gerekli tooenable FTP/S dağıtımıdır.

> [!IMPORTANT]
> Biz, sürekli olarak adımları tooimprove Microsoft Azure platformu güvenlik sürüyor. Devam eden bu çalışmaların bir parçası olarak Web uygulamaları yükseltmesini Almanya merkezi ve Almanya Kuzeydoğu bölgeler için planlanmış bir görevdir. Bu sırasında Web Apps hello dağıtımlar için düz metin FTP Protokolü kullanımını devre dışı bırakma. Öneri tooour müşterilerimizin dağıtımlar için tooswitch tooFTPS olur. Herhangi bir bozulma tooyour hizmeti için 9/5 planlandığı bu yükseltme sırasında bekliyoruz değil. Değer veriyoruz bu çaba destekler.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>1. adım: dağıtım kimlik bilgilerini ayarlama

tooaccess hello FTP sunucusu, uygulamanız için önce dağıtım kimlik bilgileri gerekir. 

Dağıtım kimlik bilgilerinizi tooset veya sıfırlama bkz [Azure uygulama hizmeti dağıtım kimlik bilgileri](app-service-deployment-credentials.md). Bu öğretici, kullanıcı düzeyinde kimlik bilgilerinin hello kullanımını gösterir.

## <a name="step-2-get-ftp-connection-information"></a>2. adım: FTP bağlantı bilgileri alma

1. Merhaba, [Azure portal](https://portal.azure.com), uygulamanızın açmak [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Seçin **genel bakış** hello soldaki menüde sonra hello değerlerini Not **FTP/dağıtım kullanıcı**, **FTP konak adı**, ve **FTPS konak adı**. 

    ![FTP bağlantı bilgileri](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Merhaba **FTP/dağıtım kullanıcı** kullanıcı değeri tarafından görüntülenen hello hello FTP sunucusu için sipariş tooprovide uygun bağlamında hello uygulama adı dahil olmak üzere Azure Portal.
    > Bulabileceğiniz seçtiğinizde aynı bilgileri hello **özellikleri** hello soldaki menüde. 
    >
    > Ayrıca, hello dağıtım parola hiçbir zaman gösterilir. Dağıtım parolanızı unutursanız, çok dön[1. adım](#step1) ve dağıtım parolanızı sıfırlayın.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Adım 3: dosyaları tooAzure dağıtma

1. FTP istemcisinden ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), vb.), tooconnect tooyour uygulama topladığınız hello bağlantı bilgisini kullanın.
3. Dosyalarınızı ve bunların ilgili dizin yapısı toohello kopyalama [ **/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) Azure (veya hello **/site/wwwroot/App_Data/işleri/** için dizin Web işleri).
4. Gözat tooyour uygulamanın URL tooverify hello uygulama düzgün çalışıyor. 

> [!NOTE] 
> Farklı [Git tabanlı dağıtımlar](app-service-deploy-local-git.md), FTP dağıtım dağıtım otomasyonlara aşağıdaki hello desteklemez: 
>
> - bağımlılık geri yükleme (örneğin, NuGet, NPM, PIP ve oluşturucu otomasyonlara)
> - .NET ikili dosyalarının derlenmesini
> - web.config nesil (burada bir [Node.js örnek](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Geri yükleme gerekir, yapı ve bu gerekli dosyalar yerel makinenizde el ile oluşturmak ve bunları uygulamanızı birlikte dağıtabilirsiniz.
>
>

## <a name="next-steps"></a>Sonraki adımlar

Daha gelişmiş dağıtım senaryoları için deneyin [tooAzure Git ile dağıtma](app-service-deploy-local-git.md). Git tabanlı dağıtım tooAzure sürüm denetimi, paket geri yüklemesi, MSBuild ve daha fazlasını sağlar.

## <a name="more-resources"></a>Daha Fazla Kaynak

* [Bir PHP MySQL web uygulaması oluşturun ve FTP dağıtmanızı](web-sites-php-mysql-deploy-use-ftp.md).
* [Azure uygulama hizmeti dağıtım kimlik bilgileri](app-service-deploy-ftp.md)
