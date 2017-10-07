---
title: Merhaba CLI gelen tooAzure aaaLog | Microsoft Docs
description: "Mac, Linux ve Windows için Azure komut satırı arabirimi (Azure CLI) hello tooyour Azure aboneliği bağlanmak"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>TooAzure hello Azure CLI gelen oturum
Hello Azure CLI, Azure kaynakları ile çalışmak için açık kaynak, platformlar arası komut kümesidir. Bu makalede Azure hesabı kimlik bilgileri tooconnect hello Azure CLI tooyour Azure aboneliği hello farklı şekillerde tooprovide açıklanır:

* Merhaba çalıştırmak `azure login` CLI komutu tooauthenticate Azure Active Directory üzerinden. Hem de tooCLI komutları bu yöntem erişmenizi [komut modları](#cli-command-modes). Merhaba komutu ek seçenekleri olmadan çalıştırdığınızda `azure login` etkileşimli bir web Portalı aracılığıyla oturum açmayı toocontinue ister. İçin ek `azure login` komutu seçenekleri, bu makale veya türü hello senaryolar görmek `azure login --help`.
* Yalnızca toouse Azure hizmet yönetimi modu CLI komutları (en yeni dağıtımlar için önerilmez) gerekiyorsa, indirin ve yayımlama ayarları dosyası, bilgisayarınıza yükleyin.

Merhaba CLI henüz yüklemediyseniz bkz [yükleme hello Azure CLI](cli-install-nodejs.md). Bir Azure aboneliğiniz yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap](http://azure.microsoft.com/free/) oluşturabilirsiniz.

Farklı bir hesap kimlikleri ve Azure abonelikleri hakkında arka plan için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Senaryo 1: etkileşimli oturum açma ile azure oturum açma
Belirli hesaplarıyla toorun gerektirir hello CLI `azure login` ve bir web tarayıcısı adı verilen bir işlem bir web portalı üzerinden hello oturum açma işlemine devam *etkileşimli oturum açma*. Bir iş veya Okul hesabı varsa, ortak bir nedeni (olarak da adlandırılan bir *kuruluş hesabı*) toorequire çok faktörlü kimlik doğrulamasını ayarlayın. Ayrıca toouse Resource Manager modunu komutları istediğinizde etkileşimli oturum açma Microsoft hesabınızla kullanın.

Etkileşimli oturum açma kolaydır: türü `azure login` ----seçenekleri olmadan hello aşağıdaki örnekte gösterildiği gibi:

```
azure login
```                                                                                             

Merhaba çıktı hello aşağıdaki gibi görünür:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Merhaba komut çıktısında tooyou sunulan hello kodu kopyalayın ve belirtilmişse tarayıcı toohttp://aka.ms/devicelogin veya diğer sayfasını açın. (Merhaba bir tarayıcıda açın aynı bilgisayara veya başka bir bilgisayara veya aygıt.) Merhaba kodu girin ve ardından istendiğinde tooenter hello kullanıcı adı ve parola misiniz hello kimliğini toouse istiyor. Bu işlem tamamlandığında hello komut kabuğu hello oturum açma işlemini tamamlar. Şöyle görünebilir:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Etkileşimli oturum açma ile kimlik doğrulaması ve yetkilendirme Azure Active Directory'yi kullanarak gerçekleştirilir. Bir Microsoft hesabı kimlik kullanırsanız, hello oturum açma işlemi, Azure Active Directory varsayılan etki alanınıza erişir. (Ücretsiz bir Azure hesabı için kaydolduysanız, Azure Active Directory'ye otomatik olarak hesabınız için varsayılan etki alanı oluşturulur.)
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>2. Senaryo: bir kullanıcı adı ve parola ile azure oturum açma
Kullanım hello `azure login` hello username komutu (`-u`) istediğiniz toouse bir iş veya Okul hesabı parametresi tooauthenticate, çok faktörlü kimlik doğrulama gerektirmez. Merhaba parolası hello komut satırında istenir (veya isteğe bağlı olarak hello parola hello ek bir parametre geçirebilir `azure login` komutu). Merhaba aşağıdaki örnek hello kullanıcı bir kurumsal hesap adını geçirir:

    azure login -u myUserName@contoso.onmicrosoft.com

Ardından olduğunuz tooenter parolanızı istenir:

    info:    Executing command login
    Password: *********

ardından Hello oturum açma işlemini tamamlar.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Bu kimlik bilgileri, ilk zaman oturum varsa tooverify sorulur kimlik doğrulama belirtecini toocache istiyor. Merhaba daha önce kullandıysanız bu istemi ayrıca oluşur `azure logout` (Merhaba makalenin sonraki bölümlerinde açıklanan) komutu. Bu istemi Otomasyon senaryoları için toobypass çalıştırma `azure login` hello ile `-q` parametresi.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Senaryo 3: bir hizmet sorumlusu ile azure oturum açma
Bir Active Directory uygulaması için bir hizmet sorumlusu oluşturmak ve hello hizmet sorumlusu, aboneliğinizde izinlere sahipse, hello kullanabilirsiniz `azure login` komutu tooauthenticate hello hizmet sorumlusu. Senaryonuza bağlı olarak, hello açık parametre olarak hello hizmet sorumlusu hello kimlik bilgilerini sağlamanız `azure login` komutu. Örneğin, hello aşağıdaki komutu hello hizmet asıl adı ve Active Directory Kiracı kimliği geçirir:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Parola istendiğinde tooprovide hello sonra size aittir. Ayrıca, CLI komut dosyası veya uygulama kod aracılığıyla hello kimlik bilgilerini sağlayın veya bir sertifika tooauthenticate hello hizmet sorumlusu etkileşimsiz Otomasyon senaryoları için kullanabilirsiniz. Ayrıntılı bilgi ve örnekler için bkz: [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Senaryo 4: yayımlama ayarları dosyası kullanın
Yalnızca toouse hello Azure hizmet yönetimi modu CLI komutları (örneğin, toodeploy Azure VM'ler hello Klasik dağıtım modelinde) gerekiyorsa, yayımlama ayarları dosyası kullanarak bağlanabilir. Bu yöntem bir sertifika hello abonelik ve hello sertifika geçerli olduğu sürece, tooperform yönetim görevleri için sağlayan yerel bilgisayarınıza yükler.

* **toodownload hello yayımlama ayarları dosyası** hesabınız için CLI yazarak Hizmet Yönetimi modunda olduğundan bu hello olun `azure config mode asm`. Ardından hello aşağıdaki komutu çalıştırın:

        azure account download

Bu varsayılan tarayıcınızı açar ve toohello toosign ister [Klasik Azure portalı](https://manage.windowsazure.com). Oturum açma, sonra bir `.publishsettings` dosya yüklemelerini. Bu dosyanın kaydedildiği yeri not edin.

> [!NOTE]
> Hesabınızın birden çok Azure Active Directory Kiracı ile ilişkili ise, Active Directory yayımlama ayarlarını toodownload istediğiniz dosya için istendiğinde tooselect olabilir.
>
>

Merhaba indirme sayfasını kullanarak seçildikten sonra veya hello Klasik Azure portalını ziyaret, hello seçili Active Directory hello Klasik portal ve indirme sayfası tarafından kullanılan hello varsayılan olur. Varsayılan kurulduktan sonra hello metni görmek '**tooreturn toohello Seçimi sayfasında burayı**' hello sayfanın üst kısmındaki hello indirme. Bağlantı tooreturn toohello Seçimi sayfasında sağlanan hello kullanın.

* **tooimport hello yayımlama ayarları dosyası**çalıştırın hello komutu aşağıdaki:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Aldıktan sonra yayımlama ayarları, hello silmelisiniz `.publishsettings` dosya. Azure CLI hello tarafından artık gerekmiyor ve kullanılan toogain erişim tooyour abonelik olabileceğinden güvenlik riski oluşturur.
>
>

## <a name="cli-command-modes"></a>CLI komut modları
Hello Azure CLI farklı komut kümeleriyle Azure kaynakları ile çalışmak için iki komut modları sağlar:

* **Resource Manager moduna** - hello Resource Manager dağıtım modelinde Azure kaynakları ile çalışmak için. tooset çalıştırmak Bu mod, `azure config mode arm`.
* **Hizmet Yönetimi modu** - hello Klasik dağıtım modelinde Azure kaynakları ile çalışmak için. tooset çalıştırmak Bu mod, `azure config mode asm`.

İlk yüklendiğinde, CLI Resource Manager modundayken hello sürümü geçerli hello.

> [!NOTE]
> Merhaba Resource Manager moduna ve hizmet yönetimi modu karşılıklı olarak birbirini dışlar. Diğer bir deyişle, bir modunda oluşturulan kaynakları hello yönetilemez diğer modu.
>
>

## <a name="multiple-subscriptions"></a>Birden çok abonelik
Birden çok Azure aboneliğiniz varsa, tooAzure bağlanırken kimlik bilgilerinizle ilişkili tooall abonelik erişim verir. Bir abonelik hello varsayılan olarak seçilen ve işlemleri gerçekleştirirken Azure CLI hello tarafından kullanılır. Merhaba abonelikleri görüntüleme hello geçerli varsayılan aboneliğe dahil olmak üzere, hello kullanarak `azure account list` komutu. Bu komut, bilgi benzer toohello aşağıdaki döndürür:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Liste önceki hello hello **geçerli** sütunu hello geçerli varsayılan abonelik Azure-alt-1 olarak gösterir. toochange hello varsayılan abonelik, kullanım hello `azure account set` komut ve toobe hello varsayılan istediğiniz hello abonelik belirtin. Örneğin:

    azure account set Azure-sub-2

Bu hello varsayılan abonelik tooAzure-alt-2 değiştirir.

> [!NOTE]
> Merhaba varsayılan abonelik değiştirme hemen etkili olur ve genel bir değişikliktir; Yeni Azure CLI komutları, bunları çalıştırmak isteyip hello aynı komut satırı örneği veya farklı bir örnek hello yeni varsayılan abonelik kullanın.
>
>

Hello Azure CLI varsayılan olmayan abonelikle toouse istiyor, ancak toochange hello geçerli varsayılan istemiyorsanız, hello kullanabilirsiniz `--subscription` seçeneği için hello komutu ve hello ad hello aboneliği hello işlemi için toouse istiyor.

Bağlı tooyour Azure aboneliğiniz olduktan sonra Azure kaynaklarıyla hello Azure CLI komutları toowork kullanmaya başlayabilirsiniz.

## <a name="storage-of-cli-settings"></a>CLI ayarlarını depolama
Oturum hello oturumunuzu `azure login` komut veya içeri aktarma yayımlama ayarları, CLI profili ve günlükleri depolanmış bir `.azure` directory bulunan, `user` dizin. `user` Dizin işletim sisteminiz tarafından korunur. Ancak, ek adımlar tooencrypt almanızı öneririz, `user` dizin. Hello yolu izleyerek yapabilirsiniz:

* Windows, hello dizin özelliklerini değiştirin veya BitLocker'ı kullanın.
* Mac üzerinde FileVault üzerinde hello dizinini açın.
* Ubuntu üzerinde hello şifreli giriş dizini özelliğini kullanın. Diğer Linux dağıtımları benzer özellikleri sunar.

## <a name="logging-out"></a>Günlük
toolog çıkışı, komutu aşağıdaki kullanım hello:

    azure logout -u <username>

Merhaba abonelikleri ilişkilendirilen hello hesabı yalnızca siler hello abonelik bilgileri hello yerel profilinden günlüğü Active Directory doğrulaması. Yayımlama ayarları dosyası da hello abonelikler için alındıysa, siler Active Directory ile ilgili bilgiler hello yerel profilinden yalnızca ancak oturum kapatılıyor.

## <a name="next-steps"></a>Sonraki adımlar
* bkz: toouse Azure CLI komutları [Kaynak Yöneticisi modunda Azure CLI komutları](virtual-machines/azure-cli-arm-commands.md) ve [Hizmet Yönetimi modunda Azure CLI komutları](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn hello Azure CLI hakkında daha fazla kaynak kodunu indirebilir, rapor sorunları veya toohello proje katkıda, hello ziyaret [hello Azure CLI için GitHub depo](https://github.com/azure/azure-xplat-cli).
* Hello Azure CLI veya Azure kullanarak sorunlarla karşılaşırsanız, hello ziyaret [Azure forumları](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
