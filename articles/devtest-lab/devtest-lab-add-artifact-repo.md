---
title: Azure DevTest Labs laboratuarda bir Git deposu ekleme | Microsoft Docs
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
ms.openlocfilehash: 053f92a65f9ae29154d471fd22ee842620b4f273
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-git-repository-to-store-custom-artifacts-and-azure-resource-manager-templates"></a>Özel yapılar ve Azure Resource Manager şablonları depolamak için bir Git deposu ekleme

İsterseniz [özel yapılar oluşturma](devtest-lab-artifact-author.md) laboratuvarınızda, VM'ler veya [bir özel test ortamı oluşturmak için Azure Resource Manager şablonlarını kullanma](devtest-lab-create-environment-from-arm.md), dahil etmek için özel bir Git deposuna eklemeniz gerekir yapıları veya ekibinizin oluşturduğu Azure Resource Manager şablonları. Depo üzerinde barındırılan [GitHub](https://github.com) veya [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Sağladık bir [Github deposunu yapılarının](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) olarak dağıtabileceğiniz-olduğu veya Laboratuvarları için özelleştirin. Özelleştirme veya bir yapıya oluşturduğunuzda, genel havuzda depolanamıyor – kendi özel depo oluşturmanız gerekir. 

Bir VM oluşturduğunuzda, Azure Resource Manager şablonu kaydetmek, istiyorsanız ve ardından daha sonra kolayca daha fazla sanal makineleri oluşturmak için kullanmak istiyorsanız özelleştirin. Özel Azure Resource Manager şablonlarınızı depolamak için kendi özel depo oluşturmanız gerekir.  

* GitHub depo oluşturmayı öğrenmek için bkz: [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* Git deposunu bir Team Services projesi oluşturmayı öğrenmek için bkz: [Visual Studio Team Services Bağlan](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Aşağıdaki ekran görüntüsünde yapıları içeren bir havuz Github'da nasıl görünebileceği örnek gösterilmektedir:  
![Örnek GitHub yapıları depo](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-the-repository-information-and-credentials"></a>Depo bilgileri ve kimlik bilgilerini alma
Laboratuvarınızı için bir depo eklemek için belirli bilgileri, depodan almanız gerekir. Aşağıdaki bölümlerde, GitHub ve Visual Studio Team Services üzerinde barındırılan depoları için bu bilgileri getirmenizde size rehberlik.

### <a name="get-the-github-repository-clone-url-and-personal-access-token"></a>GitHub depo kopya URL'si ve kişisel erişim belirteci alma
GitHub depo kopya URL'si ve kişisel erişim belirteci almak için şu adımları izleyin:

1. Yapıyı veya Azure Resource Manager şablonu tanımlarını içeren GitHub deposunu giriş sayfasına göz atın.
2. Seçin **Kopyala veya indir**.
3. Kopyalamak için düğmesini seçin **HTTPS kopyalayın url** panoya ve daha sonra kullanmak için URL kaydedin.
4. GitHub sağ üst köşesinde profilinin resmi seçin ve Seç **ayarları**.
5. İçinde **kişisel ayarları** menüsünü seçin sol taraftaki **kişisel erişim belirteçleri**.
6. Seçin **yeni belirteç Oluştur**.
7. Üzerinde **yeni kişisel erişim belirteci** want bir **belirteci açıklama**, varsayılan öğelerde kabul **kapsamı Seç**ve ardından **belirteç oluştur** .
8. Daha sonra ihtiyacınız olarak oluşturulan belirteç kaydedin.
9. GitHub artık kapatabilirsiniz.   
10. Devam [Laboratuvarınızı deposuna Bağlan](#connect-your-lab-to-the-repository) bölümü.

### <a name="get-the-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Visual Studio Team Services depo kopya URL'si ve kişisel erişim belirteci alma
Visual Studio Team Services depo kopya URL'si ve kişisel erişim belirteci almak için şu adımları izleyin:

1. Takım koleksiyonunuz giriş sayfasını açın (örneğin, `https://contoso-web-team.visualstudio.com`) ve projenizi seçin.
2. Proje giriş sayfasında seçin **kod**.
3. Projede kopya URL görüntülemek için **kod** sayfasında, **kopya**.
4. Daha sonra Bu öğreticide gerektiği URL kaydedin.
5. Kişisel erişim belirteci oluşturmak için seçin **Profilim** kullanıcı hesabı açılan menüsünden.
6. Profil bilgileri sayfasında seçin **güvenlik**.
7. Üzerinde **güvenlik** sekmesine **Ekle**.
8. İçinde **kişisel erişim belirteci oluşturma** sayfa:

   * Girin bir **açıklama** belirteci.
   * Seçin **180 gün** gelen **süresi içinde** listesi.
   * Seçin **tüm erişilebilir hesapları** gelen **hesapları** listesi.
   * Seçin **tüm kapsamlar** seçeneği.
   * Seçin **belirteç Oluştur**.
9. Tamamlandığında, yeni bir belirteç görünür **kişisel erişim belirteçleri** listesi. Seçin **kopyalama belirteci**ve daha sonra kullanmak için belirteç değeri kaydedin.
10. Devam [Laboratuvarınızı deposuna Bağlan](#connect-your-lab-to-the-repository) bölümü.

## <a name="connect-your-lab-to-the-repository"></a>Laboratuvarınızı deposuna Bağlan
1. [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.
2. Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.
3. İstenen Laboratuvar labs listesinden seçin.   
4. Sol panelde seçin **yapılandırma ve ilkeleri**.
5. Laboratuvar 's üzerinde **yapılandırma ve ilkeleri** alanında **depoları**.
6. Üzerinde **depoları** alanında **+ Ekle**.

    ![Depo düğme ekleme](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. İkinci **depoları** sayfasında, aşağıdaki bilgileri belirtin:

   * **Ad** -deposu için bir ad girin.
   * **Git kopyalama URL'si** -GitHub veya Visual Studio Team Services daha önce kopyaladığınız Git HTTPS kopya URL'sini girin.
   * **Şube** -tanımlarınızı almak için dal girin.
   * **Kişisel erişim belirteci** -daha önce aldığınız GitHub veya Visual Studio Team Services kişisel erişim belirteci girin.
   * **Klasör yolları** -, yapı veya Azure Resource Manager şablonu tanımlarını içeren kopya URL göreli en az bir klasör yolu girin. Bir alt belirtirken, klasörün yolunu eğik eklediğinizden emin olun.

     ![Depoları alanı](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. **Kaydet**’i seçin.

## <a name="next-steps"></a>Sonraki adımlar
Özel Git deponuzu oluşturduktan sonra gereksinimlerinize bağlı olarak biri veya her ikisi, aşağıdakileri yapabilirsiniz:
* Mağaza, [özel yapılar](devtest-lab-artifact-author.md), hangi daha sonra yeni sanal makineleri oluşturmak için kullanabilirsiniz.
* [Azure Resource Manager şablonları ile çoklu VM ortamları ve PaaS kaynaklarına oluşturmak](devtest-lab-create-environment-from-arm.md) ve ardından özel bağlantıların bulunması şablonları saklayın.

Bir VM oluştururken yapıları veya şablonları Git deponuzu eklenen doğrulayabilirsiniz. Bunlar, özel depo kaynağını belirtir sütununda gösterilen adını yapıları veya şablonları listesinde hemen kullanılabilir. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>İlgili blog gönderileri
* [Azure DevTest Labs yapıları başarısız olan ilgili sorunları giderme](devtest-lab-troubleshoot-artifact-failure.md)
* [Bir VM Azure DevTest Labs'de resource manager şablonu kullanarak mevcut AD etki alanına](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
