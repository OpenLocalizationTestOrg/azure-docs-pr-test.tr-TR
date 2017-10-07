---
title: Azure DevTest Labs bir Git deposu tooa laboratuvarda aaaAdd | Microsoft Docs
description: "Azure DevTest Labs'de özel yapılar kaynağınız için bir GitHub ya da Visual Studio Team Services Git deposu ekleme"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Bir Git deposu toostore özel yapılar ve Azure Resource Manager şablonları ekleyin

Çok istiyorsanız[özel yapılar oluşturma](devtest-lab-artifact-author.md) , Laboratuvar hello VM'ler için veya [Azure Resource Manager şablonları toocreate bir özel test ortamı kullanmak](devtest-lab-create-environment-from-arm.md), özel bir Git deposu tooinclude eklemeniz gerekir Merhaba yapıları veya ekibinizin oluşturduğu Azure Resource Manager şablonları. Merhaba deposu barındırılmasına [GitHub](https://github.com) veya [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Sağladık bir [Github deposunu yapılarının](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) olarak dağıtabileceğiniz-olduğu veya Laboratuvarları için özelleştirin. Özelleştirme veya bir yapıya oluşturduğunuzda, hello ortak deposunda depolanamıyor – kendi özel depo oluşturmanız gerekir. 

Bir VM oluşturduğunuzda, hello Azure Resource Manager şablonu kaydetmek, istediğiniz ve sonra kullanırsanız özelleştirme sonraki tooeasily daha fazla VM oluşturun. Özel Azure Resource Manager şablonlarınızı kendi özel depo toostore oluşturmanız gerekir.  

* toocreate GitHub deposunu nasıl görürüm toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toocreate bir Team Services projesi bir Git deposu ile nasıl görürüm toolearn [tooVisual Studio Team Services bağlanmak](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Merhaba aşağıdaki ekran görüntüsünde yapıları içeren bir havuz Github'da nasıl görünebileceği örnek gösterilmektedir:  
![Örnek GitHub yapıları depo](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Merhaba havuz bilgileri ve kimlik bilgilerini alma
tooadd depo tooyour Laboratuvar, belirli bilgileri, depodan ilk almalısınız. Aşağıdaki bölümlerde hello GitHub ve Visual Studio Team Services üzerinde barındırılan depoları için bu bilgileri getirmenizde size rehberlik.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Merhaba GitHub depo kopya URL'si ve kişisel erişim belirteci alma
tooget hello GitHub depo kopya URL'si ve kişisel erişim belirteci, şu adımları izleyin:

1. Merhaba yapı veya Azure Resource Manager şablonu tanımlarını içeren hello GitHub deposunu toohello giriş sayfasına göz atın.
2. Seçin **Kopyala veya indir**.
3. Select hello düğmesi toocopy hello **HTTPS kopyalayın url** toohello Pano ve daha sonra kullanmak için hello URL kaydedin.
4. Hello profilinin resmi hello sağ üst köşesinde GitHub seçip **ayarları**.
5. Merhaba, **kişisel ayarları** menüsünde sol hello select **kişisel erişim belirteçleri**.
6. Seçin **yeni belirteç Oluştur**.
7. Merhaba üzerinde **yeni kişisel erişim belirteci** want bir **belirteci açıklama**, hello hello varsayılan öğeleri kabul **kapsamı Seç**ve ardından **oluştur Belirteç**.
8. Daha sonra ihtiyacınız olarak oluşturulan hello belirteci kaydedin.
9. GitHub artık kapatabilirsiniz.   
10. Toohello devam [Laboratuvar toohello deponuza bağlamak](#connect-your-lab-to-the-repository) bölümü.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Merhaba Visual Studio Team Services depo kopya URL'si ve kişisel erişim belirteci alma
tooget hello Visual Studio Team Services depo kopya URL'si ve kişisel erişim belirteci, şu adımları izleyin:

1. Takım koleksiyonunun açık hello giriş sayfası (örneğin, `https://contoso-web-team.visualstudio.com`) ve projenizi seçin.
2. Merhaba proje giriş sayfasında, seçin **kod**.
3. Merhaba projede tooview hello kopya URL **kod** sayfasında, **kopya**.
4. Daha sonra Bu öğreticide gerektiği hello URL kaydedin.
5. bir kişisel erişim belirteci, toocreate seçin **Profilim** hello kullanıcı hesabı açılan menüsünden.
6. Hello profil bilgileri sayfasında seçin **güvenlik**.
7. Merhaba üzerinde **güvenlik** sekmesine **Ekle**.
8. Merhaba, **kişisel erişim belirteci oluşturma** sayfa:

   * Girin bir **açıklama** hello belirteci.
   * Seçin **180 gün** hello gelen **süresi içinde** listesi.
   * Seçin **tüm erişilebilir hesapları** hello gelen **hesapları** listesi.
   * Merhaba seçin **tüm kapsamlar** seçeneği.
   * Seçin **belirteç Oluştur**.
9. Tamamlandığında, hello yeni belirteci hello görünür **kişisel erişim belirteçleri** listesi. Seçin **kopyalama belirteci**ve ardından hello belirteç değeri daha sonra kullanmak için kaydedin.
10. Toohello devam [Laboratuvar toohello deponuza bağlamak](#connect-your-lab-to-the-repository) bölümü.

## <a name="connect-your-lab-toohello-repository"></a>Laboratuvar toohello deponuz Bağlan
1. İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** hello listeden.
3. Merhaba istenen Laboratuvar labs Hello listeden seçin.   
4. Merhaba sol panelinde seçin **yapılandırma ve ilkeleri**.
5. Merhaba Laboratuvar'ın üzerinde **yapılandırma ve ilkeleri** alanında **depoları**.
6. Merhaba üzerinde **depoları** alanında **+ Ekle**.

    ![Depo düğme ekleme](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. Merhaba üzerinde ikinci **depoları** sayfasında, aşağıdaki bilgilerle hello belirtin:

   * **Ad** -hello deposu için bir ad girin.
   * **Git kopyalama URL'si** -GitHub veya Visual Studio Team Services daha önce kopyaladığınız hello Git HTTPS kopya URL'si girin.
   * **Şube** -tanımlarınızı hello şube tooget girin.
   * **Kişisel erişim belirteci** -daha önce aldığınız GitHub veya Visual Studio Team Services hello kişisel erişim belirteci girin.
   * **Klasör yolları** -, yapı veya Azure Resource Manager şablonu tanımlarını içeren en az bir klasör yolu göreli toohello kopya URL'si girin. Bir alt belirtirken emin tooinclude hello eğik hello klasör yolu olun.

     ![Depoları alanı](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. **Kaydet**’i seçin.

## <a name="next-steps"></a>Sonraki adımlar
Özel Git deponuzu oluşturduktan sonra gereksinimlerinize bağlı olarak birini veya her ikisini hello şunları yapabilirsiniz:
* Mağaza, [özel yapılar](devtest-lab-artifact-author.md), hangi sonraki toocreate kullanabileceğiniz yeni VM'ler.
* [Azure Resource Manager şablonları ile çoklu VM ortamları ve PaaS kaynaklarına oluşturmak](devtest-lab-create-environment-from-arm.md) ve ardından özel bağlantıların bulunması hello şablonları saklayın.

Bir VM oluştururken hello yapıları veya şablonları tooyour Git deposu eklenen doğrulayabilirsiniz. Bunlar, hemen listesinde hello yapıları veya şablonlarını hello kaynağını belirtir hello sütununda gösterilen özel, depodaki hello adı ile kullanılabilir. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>İlgili blog gönderileri
* [Nasıl tootroubleshoot Azure DevTest Labs yapıları başarısız](devtest-lab-troubleshoot-artifact-failure.md)
* [VM tooexisting AD Azure DevTest Labs'de resource manager şablonu kullanarak etki alanına katılma](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
