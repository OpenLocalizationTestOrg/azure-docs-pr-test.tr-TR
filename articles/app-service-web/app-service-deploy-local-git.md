---
title: "aaaLocal Git dağıtımı tooAzure uygulama hizmeti"
description: "Bilgi nasıl tooenable yerel Git dağıtım tooAzure uygulama hizmeti."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>Yerel Git dağıtımı tooAzure uygulama hizmeti
Bu öğretici şunların nasıl yapıldığını gösterir toodeploy uygulamanızı çok[Azure App Service] yerel bilgisayarınızdaki bir Git deposundan. Uygulama hizmetini destekleyen hello bu yaklaşımı **yerel Git** hello dağıtım seçeneği [Azure Portal].  
Bu makalede açıklanan hello Git komutların çoğu hello kullanarak bir uygulama hizmeti uygulaması oluştururken, otomatik olarak gerçekleştirilir [Azure komut satırı arabirimi] açıklandığı gibi [burada](app-service-web-get-started.md).

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğretici, gerekir:

* Git. Merhaba yükleme ikili indirebilirsiniz [burada](http://www.git-scm.com/downloads).  
* Git temel bilgiye.
* Bir Microsoft Azure hesabı. Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.  
> 
> 

## <a name="Step1"></a>1. adım: yerel bir havuz oluşturma
Aşağıdaki görevler toocreate yeni bir Git deposu hello gerçekleştirin.

1. Bir komut satırı aracı gibi başlatın **Gitbash'i** (Windows) veya **Bash** (UNIX kabuğu). OS X sistemleri üzerinde hello komut satırı hello erişebilirsiniz **Terminal** uygulama.
2. Merhaba içerik toodeploy bulunduğu olduğu toohello dizinine gidin.
3. Komut tooinitialize yeni bir Git deposu aşağıdaki hello kullan:

```bash  
git init
```

## <a name="Step2"></a>2. adım: içeriğinizi Yürüt
Uygulama hizmeti çeşitli programlama dillerini içinde oluşturulan uygulamaları destekler. 

1. Deponuzda zaten içerik Atla içeriyorsa, bu işaret ve toopoint 2 aşağıdaki taşıyın. Deponuzda zaten içeriği yalnızca içermiyorsa statik .html dosyasıyla gibi doldurun: 
   
   * Bir metin düzenleyicisi kullanarak adlı yeni bir dosya oluşturun **index.html** hello Git deposunu hello kökü
   * Hello içeriği hello index.html için dosya ve kaydedin gibi metin aşağıdaki hello ekleyin: *Hello Git!*
2. Komut satırı Hello, Git deponuzu hello kök altında olduğundan emin olun. Ardından komutu tooadd dosyaları tooyour deposu aşağıdaki hello kullanın:

```bash  
git add -A
```
3. Ardından, komutu aşağıdaki hello kullanarak hello değişiklikleri toohello depo Yürüt:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>3. adım: hello uygulama hizmeti uygulama havuzu etkinleştir
Aşağıdaki adımları tooenable App Service uygulamanız için bir Git deposu hello gerçekleştirin.

1. İçinde toohello oturum [Azure Portal].
2. App Service uygulamanızın dikey penceresinde tıklayın **ayarlar > dağıtım kaynağı**. Tıklatın **Kaynak Seç**, ardından **yerel Git deposu**ve ardından **Tamam**.  
   
    ![Yerel Git deposu](./media/app-service-deploy-local-git/local_git_selection.png)
3. İlk zaman ayarınız Azure deposunu varsa, toocreate oturum açma kimlik bilgileri için gerekir. Bunları hello Azure deposunu içine toolog ve anında iletme değişiklikler yerel Git deposundan kullanın. Uygulamanızın dikey penceresinden tıklayın **ayarlar > Dağıtım kimlik bilgileri**, dağıtım kullanıcı adı ve parola yapılandırın. İşiniz bittiğinde tıklatın **kaydetmek**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Adım 4: projenizi dağıtma
Aşağıdaki adımları toopublish Merhaba, uygulama tooApp yerel Git kullanarak hizmeti kullanın.

1. Hello Azure Portalı'nda, uygulamanızın dikey penceresinde tıklayın **ayarlar > Özellikler** hello için **Git URL'si**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **Git URL'si** hello uzak başvuru toodeploy toofrom, yerel bir depodur. Bu URL aşağıdaki adımları hello kullanacaksınız.
2. Merhaba komut satırı kullanarak, yerel Git deponuzu hello kök dizininde olduğundan emin olun.
3. Kullanım `git remote` tooadd hello uzak başvuru listelenen **Git URL'si** adım 1. Komutunuzu benzer toohello aşağıdaki görünür:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Merhaba **uzak** komut adlandırılmış başvuru tooa uzak bir depo ekler. Bu örnekte, web uygulamanızın depo için 'azure' adlı bir başvuru oluşturur.
   > 
   > 
4. İçerik tooApp hizmet itme hello kullanarak yeni **azure** uzak oluşturduğunuz.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Hello Azure Portal tooyour uygulamaya geri dönün. En son gönderme, bir günlük girişi hello görüntülenmelidir **dağıtımları** dikey. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Merhaba tıklatın **Gözat** düğmesi hello uygulamanın dikey tooverify hello içerik hello üstündeki dağıtılan. 

## <a name="Step5"></a>Sorun giderme
Merhaba Git toopublish tooan App Service uygulaması Azure'da kullanırken sık karşılaşılan sorunları veya hatalar şunlardır:

- - -
**Belirti**: oluşturulamıyor tooaccess [siteURL]: tooconnect çok başarısız [scmAddress]

**Neden**: hello uygulama hazır ve çalışır değilse bu hata oluşabilir.

**Çözümleme**: Başlangıç hello hello Azure Portal uygulamasında. Merhaba uygulama çalışmıyorsa Git dağıtımı çalışmaz. 

- - -
**Belirti**: ana bilgisayar 'hostname' çözümleyemedik

**Neden**: hello adres bilgilerini oluştururken girdiyseniz bu hata hello 'azure' uzak yanlış oluşabilir.

**Çözümleme**: kullanım hello `git remote -v` toolist hello ilişkili URL ile birlikte tüm uzaktan kumandalar komutu. Merhaba 'azure' uzak Hello URL'sini doğru olduğundan emin olun. Gerekirse, kaldırın ve bu uzak hello doğru URL'yi kullanarak oluşturun.

- - -
**Belirti**: ortak hiçbir refs ve hiçbiri belirtilen; hiçbir şey yapılması. Belki 'master' gibi bir dal belirtmeniz gerekir.

**Neden**:, değil git itme işlemi gerçekleştirirken bir dal belirtin ve Git tarafından kullanılan ayarlanmamış hello push.default değerine varsa bu hata oluşabilir.

**Çözümleme**: hello ana dala belirtme hello gönderme işlemi yeniden gerçekleştirin. Örneğin:

```bash  
git push azure master
```
- - -
**Belirti**: src refspec [branchname] herhangi eşleşmiyor.

**Neden**: toopush tooa şube hello 'azure' uzak yöneticisinde dışında çalışırsanız, bu hata oluşabilir.

**Çözümleme**: hello ana dala belirtme hello gönderme işlemi yeniden gerçekleştirin. Örneğin:

```bash  
git push azure master
```
- - -
**Belirti**: RPC başarısız oldu; yol = 22, HTTP kodu 502 =.

**Neden**: HTTPS üzerinden toopush büyük git deposu çalışırsanız, bu hata oluşabilir.

**Çözümleme**: hello yerel makine toomake hello postBuffer büyük üzerinde hello git yapılandırmasını değiştirme

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Belirti**: hata - web uygulamanızı güncelleştirilmemiş ancak değişiklikleri taahhüt tooremote deposu.

**Neden**: ek gerekli modüllerini belirten bir package.json dosyası içeren bir Node.js uygulaması dağıtıyorsanız bu hata oluşabilir.

**Çözümleme**: 'npm hata!' içeren ek iletiler günlüğe kaydedilen önceki toothis hata olmalıdır ve ek bağlam hello hatada sağlayabilir. Merhaba aşağıdaki bu hatanın nedeni bilinen ve karşılık gelen 'npm hata!' hello İleti:

* **Hatalı biçimlendirilmiş package.json dosyası**: npm hata! Bağımlılıklar okunamadı.
* **İkili bir dağıtım için Windows olmayan yerel modül**:
  
  * npm hata! \`cmd "/ c" "düğümü gyp yeniden oluşturma"\` 1 ile başarısız oldu
    
      OR
  * npm hata! [modulename@version] önceden: \`olun || gmake\`

## <a name="additional-resources"></a>Ek Kaynaklar
* [Git belgeleri](http://git-scm.com/documentation)
* [Proje Kudu belgeleri](https://github.com/projectkudu/kudu/wiki)
* [Sürekli dağıtım tooAzure uygulama hizmeti](app-service-continuous-deployment.md)
* [Nasıl toouse Azure PowerShell](/powershell/azure/overview)
* [Nasıl toouse hello Azure komut satırı arabirimi](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure komut satırı arabirimi]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
