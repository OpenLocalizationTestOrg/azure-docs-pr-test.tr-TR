---
title: "Azure işlevleri için aaaContinuous dağıtımı | Microsoft Docs"
description: "Azure uygulama hizmeti toopublish, sürekli dağıtım özellikleri, Azure işlevlerini kullanın."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Azure İşlevleri için sürekli dağıtım
Azure işlevleri kılar kolay toodeploy uygulama hizmeti sürekli tümleştirme kullanarak işlevi uygulamanızı. İşlevler, BitBucket, Dropbox, GitHub ve Visual Studio Team Services (VSTS) ile tümleşir. Bu Tümleşik Hizmetler tetikleyici dağıtım tooAzure birini kullanarak yapılan burada işlev kodu güncelleştirmeleri bir iş akışı sağlar. Yeni tooAzure işlevleri varsa, başlayın [Azure işlevlerine genel bakış](functions-overview.md).

Sürekli dağıtım, birden fazla ve sık gerçekleşen katkıların tümleştirildiği projeler için mükemmel bir seçenektir. Ayrıca, kaynak denetimi işlevleri kodunuzu tutmanıza sağlar. Aşağıdaki dağıtım kaynaklar hello şu anda desteklenir:

* [Bitbucket](https://bitbucket.org/)
* [Açılan kutu](https://www.dropbox.com/)
* Dış depo (Git veya Mercurial)
* [Yerel Git deposu](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Dağıtımları bir işlev başına uygulama temelinde yapılandırılır. Sürekli dağıtım etkinleştirildikten sonra erişim toofunction kod hello portalında çok kümesi*salt okunur*.

## <a name="continuous-deployment-requirements"></a>Sürekli dağıtım gereksinimleri

Yapılandırılan dağıtım kaynağınız ve işlevleri kodunuz hello dağıtım kaynağı, sürekli dağıtım ayarlayın. önce olmalıdır. Verilen işlevin uygulama dağıtımı her işlevi hello dizin adı hello işlevinin hello adı olduğu bir adlandırılmış alt dizininde bulunur.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Sürekli dağıtım ayarlama
Bu yordam tooconfigure sürekli dağıtımı için var olan bir işlev uygulaması kullanın. GitHub depo ile tümleştirme adımları gösterir, ancak Visual Studio Team Services veya diğer Dağıtım Hizmetleri için benzer adımları uygulayın.

1. Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım seçenekleri**. 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Merhaba sonra **dağıtımları** dikey penceresinde **Kurulum**.
 
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Merhaba, **dağıtım kaynağı** dikey penceresinde tıklatın **Kaynak Seç**, seçtiğiniz dağıtım kaynağınız hello bilgileri doldurun ve **Tamam**.
   
    ![Dağıtım kaynağı seçin](./media/functions-continuous-deployment/choose-deployment-source.png)

Sürekli dağıtım yapılandırıldıktan sonra tüm dosya değişiklikler dağıtım kaynağınızda kopyalanan toohello işlev uygulaması ve bir sitenin tam dağıtım tetiklenir. Merhaba kaynak dosyalarında güncelleştirildiğinde hello site yeniden dağıtıldı.

## <a name="deployment-options"></a>Dağıtım seçenekleri

Merhaba, bazı tipik dağıtım senaryoları şunlardır:

- [Hazırlama dağıtımı oluşturma](#staging)
- [Var olan işlevler toocontinuous dağıtımını taşıma](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Hazırlama dağıtımı oluşturma

İşlev uygulamalar henüz dağıtım yuvaları desteklemiyor. Ancak, yine de, sürekli tümleştirme kullanarak ayrı hazırlama ve üretim dağıtımları yönetebilirsiniz.

işlem tooconfigure hello ve iş hazırlama dağıtımıyla genellikle şöyle görünür:

1. Aboneliğiniz, hello üretim kodu için diğeri için hazırlama iki işlevi uygulamalar oluşturun. 

2. Zaten yoksa, bir dağıtım kaynağı oluşturun. Bu örnekte [GitHub].

3. Üretim işlevi uygulamanız için tam hello önceki bölümlerinde bulunan adımları **sürekli dağıtım ayarlayın** ve kümesi hello dağıtım şube toohello ana, GitHub deponun dalı.
   
    ![Dağıtım şube seçin](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. İşlev uygulaması hazırlama hello için bu adımı yineleyin, ancak dal, bunun yerine, GitHub deposuna hazırlama hello seçin. Dağıtım kaynağı dallanma desteklemiyorsa, farklı bir klasör kullanın.
    
5. Güncelleştirmeleri tooyour Kodu'nu şube veya klasörün hazırlama hello sonra bu değişiklikleri dağıtım hazırlama hello yansıtılır doğrulayın.

6. Test sonra birleştirme hello ana dala hello hazırlama daldan değiştirir. Bu birleştirme dağıtım toohello üretim işlev uygulaması tetikler. Dağıtım kaynağı dalları desteklemiyorsa, hello üretim klasöründeki hello dosyaları klasörü hazırlama hello hello dosyalarından üzerine yazın.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Var olan işlevler toocontinuous dağıtımını taşıma
Oluşturulmuş ve korunan hello Portalı'nda toodownload ihtiyacınız var olan işlevler varsa, yukarıda açıklandığı gibi sürekli dağıtım ayarlamadan önce FTP veya hello yerel Git deposu kullanarak kod dosyaları işlev varolan. Hello App Service ayarlarını işlevi uygulamanız için bunu yapabilirsiniz. Dosyalarınızı İndirildikten sonra seçilen tooyour sürekli dağıtım kaynağı karşıya yükleyebilirsiniz.

> [!NOTE]
> Sürekli Tümleştirme yapılandırdıktan sonra artık hello işlevleri Portalı'nda, kaynak dosyaları mümkün tooedit olacaktır.

- [Nasıl yapılır: dağıtım kimlik bilgilerini yapılandırın](#credentials)
- [Nasıl yapılır: FTP kullanarak dosyaları indirme](#downftp)
- [Nasıl yapılır: hello yerel Git deposu kullanarak dosyaları indirme](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Nasıl yapılır: dağıtım kimlik bilgilerini yapılandırın
FTP veya yerel Git deposu ile işlevi uygulamanızdan dosyalarını indirmeden önce kimlik bilgilerini tooaccess hello sitenizi yapılandırmanız gerekir. Kimlik bilgileri hello işlevi uygulama düzeyinde ayarlanır. Hello Azure portal adımları tooset dağıtım kimlik bilgilerini aşağıdaki hello kullan:

1. Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım kimlik bilgileri**.
   
    ![Yerel dağıtım kimlik bilgilerini ayarlama](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Bir kullanıcı adı ve parolasını yazın ve ardından **kaydetmek**. Bu gibi durumlarda, bu kimlik bilgileri tooaccess şimdi işlevi uygulamanızdan FTP veya hello yerleşik Git deposu kullanabilirsiniz.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Nasıl yapılır: FTP kullanarak dosyaları indirme

1. Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **özellikleri**, hello değerlerini kopyalayın **FTP/dağıtım kullanıcı**, **FTP ana bilgisayar adı**, ve **FTPS konak adı**.  

    **FTP/dağıtım kullanıcısı** hello uygulama adı, tooprovide uygun bağlamı hello FTP sunucusu için de dahil olmak üzere hello portalında görüntülenen girilmelidir.
   
    ![Dağıtım bilgileri alma](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. FTP istemcisinden, tooconnect tooyour uygulama topladığınız hello bağlantı bilgilerini kullanın ve işlevlerinizi hello kaynak dosyalarını indirin.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Nasıl yapılır: yerel bir Git deposu kullanarak dosyaları indirme

1. Merhaba işlevi uygulamanızda [Azure portal](https://portal.azure.com), tıklatın **Platform özellikleri** ve **dağıtım seçenekleri**. 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Merhaba sonra **dağıtımları** dikey penceresinde **Kurulum**.
 
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Merhaba, **dağıtım kaynağı** dikey penceresinde tıklatın **yerel Git deposu** ve ardından **Tamam**.

3. İçinde **Platform özellikleri**, tıklatın **özellikleri** ve Git URL'si hello değerini not edin. 
   
    ![Sürekli dağıtım ayarlayın](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Git algılayan bir komut istemi veya sık kullanılan Git aracı kullanarak yerel makinenizde Hello depoyu kopyalayın. Merhaba Git kopya komut şöyle görünür:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Dosyaları aşağıdaki örneğine hello olduğu gibi yerel bilgisayarınızda, işlev uygulaması toohello kopya getirin:
   
        git pull origin master
   
    İstenirse, sağlamanız, [dağıtım kimlik bilgileri yapılandırılmış](#credentials).  

[GitHub]: https://github.com/
