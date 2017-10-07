---
title: aaaCreate Azure Jenkins sunucuda
description: "Merhaba Jenkins çözüm şablonu Azure Linux sanal makineden Jenkins yükleyin ve bir örnek Java uygulaması oluşturma."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Azure Linux VM'de hello Azure Portalı'ndan bir Jenkins sunucu oluşturma

Bu hızlı başlangıç gösterir nasıl tooinstall [Jenkins](https://jenkins.io) hello Araçlar ve eklentiler yapılandırılmış toowork Ubuntu Linux VM'de Azure ile. İşlemi tamamladığınızda, Azure‘da çalışan bir Jenkins sunucusuna sahip ve [GitHub](https://github.com)’dan örnek bir Java uygulaması oluşturmuş olursunuz.

## <a name="prerequisites"></a>Ön koşullar

* Bir Azure aboneliği
* Bilgisayarınızın komut satırında erişim tooSSH (Merhaba gibi Kabuk Bash veya [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Merhaba Jenkins VM hello çözüm Şablondan Oluştur

Açık hello [Market görüntüsü için Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) web tarayıcısı ve seçin **BT almak artık** hello sayfasının sol taraftaki hello. Gözden geçirme hello fiyatlandırma ayrıntıları ve select **devam**seçeneğini belirleyip **oluşturma** tooconfigure hello Jenkins hello Azure portal Server'da. 
   
![Azure portalı iletişim kutusu](./media/install-jenkins-solution-template/ap-create.png)

Merhaba, **temel ayarları yapılandırmanız** sekmesinde, hello aşağıdaki alanları doldurun:

![Temel ayarları yapılandırma](./media/install-jenkins-solution-template/ap-basic.png)

* **Ad** olarak **Jenkins** yazın.
* Bir **Kullanıcı adı** girin. Merhaba kullanıcı adı karşılamalıdır [belirli gereksinimleri](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Seçin **parola** hello olarak **kimlik doğrulama türü** ve bir parola girin. Merhaba parolası, bir büyük harf karakter, sayı ve bir özel karakter olmalıdır.
* Kullanım **myJenkinsResourceGroup** hello için **kaynak grubu**.
* Merhaba seçin **Doğu ABD** [Azure bölgesi](https://azure.microsoft.com/regions/) hello gelen **konumu** açılır.

Seçin **Tamam** tooproceed toohello **ek seçenekleri yapılandırmak** sekmesi. Benzersiz etki alanı adı tooidentify hello Jenkins sunucusu girin ve **Tamam**.

![Ek seçenekleri ayarlama](./media/install-jenkins-solution-template/ap-addtional.png)  

 Doğrulama başarılı sonra seçeneğini **Tamam** yeniden hello gelen **Özet** sekmesi. Son olarak, seçin **satın alma** toocreate hello Jenkins VM. Sunucunuz hazır olduğunda, hello Azure portalında bir bildirim alın:   

![Jenkins hazır bildirimi](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>TooJenkins Bağlan

Web tarayıcınızda tooyour sanal makine (örneğin, http://jenkins2517454.eastus.cloudapp.azure.com/) gidin. Merhaba Jenkins konsol güvenli olmayan HTTP erişilemez olduğundan hello sayfa tooaccess hello Jenkins konsolunda bilgisayarınızdan SSH tüneli kullanarak güvenli bir şekilde yönergeler sağlanmıştır.

![Jenkins’in kilidini açma](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Hello kullanarak hello tünel ayarlamak `ssh` hello komut satırından hello sayfasında komutu değiştirme `username` hello hello sanal Makine'yi hello çözüm şablondan ayarlarken daha önce seçilen hello sanal makine yönetici kullanıcı adı.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Merhaba tünel başlattıktan sonra toohttp://localhost:8080 gidin / yerel makinenizde. 

Merhaba ilk parola hello komut satırında SSH toohello Jenkins VM bağlıyken komutu aşağıdaki hello çalıştırarak alın.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Merhaba Hello Jenkins panosunu ilk bu parolayı kullanarak ilk kez kilidini açın.

![Jenkins’in kilidini açma](./media/install-jenkins-solution-template/jenkins-unlock.png)

Seçin **önerilen Eklentileri yüklemek** hello sonraki sayfa ve bir Jenkins yönetici kullanıcı kullanılan tooaccess hello Jenkins pano oluşturun.

![Jenkins hazır!](./media/install-jenkins-solution-template/jenkins-welcome.png)

Merhaba Jenkins sunucu şimdi hazır toobuild kodudur.

## <a name="create-your-first-job"></a>İlk işinizi oluşturma

Seçin **yeni iş oluşturma** hello Jenkins konsolundan adını **mySampleApp** seçip **Serbest stilde proje**seçeneğini belirleyip **Tamam**.

![Yeni bir iş oluşturma](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Select hello **kaynak kodu Yönetimi** sekmesinde, etkinleştirme **Git**, URL'de aşağıdaki hello girin **depo URL'si** alan:`https://github.com/spring-guides/gs-spring-boot.git`

![Merhaba Git deposuna tanımlayın](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Select hello **yapı** sekmesini ve ardından **Ekle derleme adımı**, **çağırma Gradle betik**. **Gradle sarmalayıcıyı kullan**’ı seçin, ardından **Sarmalayıcı konumu**’na `complete` değerini, **Görevler** için `build` değerini girin.

![Merhaba Gradle sarmalayıcı toobuild kullanın](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

**Gelişmiş...**’i seçin ve ardından girin `complete` hello içinde **kök yapı betik** alan. **Kaydet**’i seçin.

![Merhaba Gradle sarmalayıcı yapı adımda Gelişmiş ayarlar](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Merhaba kodu derleme

Seçin **şimdi yapı** toocompile hello kodu ve paket hello örnek uygulama. Merhaba, yapı tamamlandıktan sonra seçin **çalışma** hello projesi için bağlantı.

![Toohello çalışma tooget hello JAR dosyasını hello yapıdan Gözat](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Çok gidin`complete/build/libs` ve hello olun `gs-spring-boot-0.1.0.jar` yapınızın başarılı tooverify yoktur. Sunucu artık oldu, Jenkins toobuild kendi Azure projelerinde hazır.

## <a name="next-steps"></a>Sonraki Adımlar

> [!div class="nextstepaction"]
> [Jenkins aracıları olarak Azure VM'leri ekleme](jenkins-azure-vm-agents.md)
