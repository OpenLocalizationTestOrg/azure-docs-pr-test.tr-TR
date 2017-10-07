---
title: "Azure mikro için sürekli tümleştirme aaaSet | Microsoft Docs"
description: "Nasıl bir bakış elde tooset sürekli tümleştirme ve dağıtım için Visual Studio Team Services (VSTS) kullanarak bir Service Fabric uygulaması."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Service Fabric sürekli tümleştirme ve Visual Studio Team Services ile dağıtımı ayarlama
Bu makalede, Visual Studio Team Services (VSTS) kullanarak hello adımları tooset sürekli tümleştirme ve bir Azure Service Fabric uygulaması için dağıtım açıklanmaktadır.

Bu belge hello geçerli yordamı yansıtır ve beklenen toochange Zamanla.

## <a name="prerequisites"></a>Ön koşullar
tooget başlatıldı, şu adımları izleyin:

1. Erişim tooa Team Services hesabı olduğundan emin olun veya [oluşturmak](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) kendiniz.
2. Erişim tooa Team Services takım projesine sahip olduğundan emin olun veya [oluşturmak](https://www.visualstudio.com/docs/setup-admin/create-team-project) kendiniz.
3. Uygulamanızı dağıtmak veya bir tane oluşturun bir Service Fabric kümesi toowhich sahip olduğundan emin olun hello kullanarak [Azure portal](service-fabric-cluster-creation-via-portal.md), bir [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md), veya [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Bir Service Fabric uygulaması (.sfproj) projesi oluşturmuş emin olun. Oluşturulmuş veya Service Fabric SDK 2.1 veya üzeri yükseltilmiş bir proje olmalıdır (Merhaba .sfproj dosya 1.1 veya üzeri bir ProjectVersion özellik değeri içermelidir).

> [!NOTE]
> Özel derleme aracıları artık gerekli değildir. Team Services şimdi Service Fabric küme yönetimi yazılımını ile önceden yüklenmiş olarak gelen aracıları doğrudan bu aracıların, uygulamaların dağıtımını izin vermeyi barındırılan.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Yapılandırma ve kaynak dosyaları paylaşma
Merhaba ilk şey toodo olan istediğiniz Team Services içinde yürütür hello dağıtım işlemi tarafından kullanım için bir yayımlama profili hazırlayın.  Merhaba yayımlama profili önceden hazırladığınız yapılandırılmış tootarget hello kümesine olması gerekir:

1. Bir yayımlama profili, uygulama projesi içinde sürekli tümleştirme iş akışınız için toouse istediğinizi seçin. Merhaba izleyin [yönergeleri yayımlama](service-fabric-publish-app-remote-cluster.md) nasıl toopublish bir uygulama tooa uzaktan küme. Aslında toopublish uygulamanız yine de ihtiyacınız yoktur. Merhaba tıklayabilirsiniz **kaydetmek** hello köprü Yayımla iletişim şeyler uygun şekilde yapılandırdıktan sonra.
2. Team Services içinde oluşan her bir dağıtım için yükseltme, uygulama toobe istiyorsanız, tooconfigure hello istediğiniz profili tooenable yükseltme yayımlayın. 1. adımda aynı yayımlama kullanılan iletişim hello bu hello olun **yükseltme hello uygulama** onay kutusu işaretli.  Daha fazla bilgi edinmek [ek yükseltme ayarlarını yapılandırma](service-fabric-visualstudio-configure-upgrade.md). Merhaba tıklatın **kaydetmek** köprü toosave hello ayarları toohello yayımlama profili.
3. Değişikliklerinizi toohello yayımlama profili kaydettiğiniz ve hello iptal olun yayımlama iletişim kutusu.
4. Zaman çok. Şimdi[uygulama projesi kaynak dosyaları paylaşma](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) Team Services ile. Kaynak dosyalarınız Team Services içinde erişilebilir olduktan sonra artık derlemeleri oluşturma toohello sonraki adımda taşıyabilirsiniz. 

## <a name="create-a-build-definition"></a>Yapı tanımı oluşturma
Bir Team Services yapı tanımı sırayla yürütülen derleme adımları kümesinden oluşan bir iş akışını açıklar. Merhaba oluşturmakta olduğunuz hello derleme tanımı tooproduce bir Service Fabric uygulama paketi ve kullanılan toodeploy Merhaba uygulaması olabilecek diğer yapıları hedefidir. Team Services hakkında daha fazla bilgi [yapı tanımları](https://www.visualstudio.com/docs/build/define/create).

### <a name="create-a-definition-from-hello-build-template"></a>Merhaba yapı şablonundan bir tanımı oluşturun
1. Takım projenizin Visual Studio Team Services içinde açın.
2. Select hello **yapı** sekmesi.
3. Select hello yeşil  **+**  toocreate yeni bir derleme tanımınız oturum açın.
4. Açılır hello iletişim kutusunda seçin **Azure Service Fabric uygulaması** hello içinde **yapı** şablon kategorisi.
5. Seçin **sonraki**.
6. Merhaba depo ve Service Fabric uygulamanızla ilişkili dalı seçin.
7. Merhaba aracı sıra toouse istediğiniz seçin. Barındırılan aracılar desteklenir.
8. **Oluştur**’u seçin.
9. Merhaba derleme tanımını kaydedin ve bir ad sağlayın.
10. Merhaba aşağıdaki paragraf hello derleme adımları hello şablon tarafından oluşturulan bir açıklaması verilmiştir:

| Adım oluşturma | Açıklama |
| --- | --- |
| NuGet geri yükleme |Merhaba hello çözüm için NuGet paketlerini geri yükler. |
| Çözümü derlemek \*.sln |Çözümün tamamında Hello oluşturur. |
| Çözümü derlemek \*.sfproj |Kullanılan toodeploy hello uygulama hello Service Fabric uygulama paketi oluşturur. Merhaba yapı yapı dizini içinde belirtilen toobe Hello uygulama paketi konumdur. |
| Güncelleştirme hizmeti doku uygulama sürümleri |Merhaba uygulama paketin bildirim dosyaları tooallow yükseltme desteği bulunan hello sürümüne güncelleştirir. Merhaba bkz [görev belge sayfasının](https://go.microsoft.com/fwlink/?LinkId=820529) daha fazla bilgi için. |
| Dosyaları kopyalama |Kopya hello profili ve dağıtımı için kullanılan uygulama parametreleri dosyalarını toohello yapı yapıları toobe yayımlayın. |
| Yapı yayımlama |Merhaba yapı yapıları yayımlar. Bir yayın tanımı tooconsume hello yapı yapıları sağlar. |

### <a name="verify-hello-default-set-of-tasks"></a>Merhaba varsayılan görevler kümesini doğrulayın
1. Merhaba doğrulayın **çözüm** hello giriş alanını **NuGet restore** ve **yapı çözümü** derleme adımları.  Varsayılan olarak, bu derleme adımları ilişkili hello deposunda bulunan tüm çözüm dosyalarını üzerine yürütün.  Bu çözüm dosyaları birinde hello derleme tanımı toooperate yalnızca istiyorsanız, tooexplicitly güncelleştirme hello yol toothat dosyası gerekir.
2. Merhaba doğrulayın **çözüm** hello giriş alanını **Uygulama paketleme** adım oluşturma.  Varsayılan olarak, yalnızca bir Service Fabric uygulaması projesi (.sfproj) hello deposunda mevcut bu derleme adımı varsayar.  Depoda yerini birden çok dosya varsa ve bu derleme tanımı için bunlardan yalnızca birini tootarget istediğiniz tooexplicitly güncelleştirme hello yol toothat dosyası gerekir.  Deponuzda içinde birden çok uygulama projeleri toopackage istiyorsanız, toocreate ek gereksinim **Visual Studio derleme** her bir uygulama proje hedef hello derleme tanımı'nda adımları.  Ardından tooupdate hello ayrıca gerekir **MSBuild bağımsız değişkenleri** bunların her biri için alan oluşturmak adımları hello paket konumu bunların her biri için benzersiz olmasını sağlayın.
3. Hello tanımlanan hello sürüm oluşturma davranışı doğrulayın **güncelleştirme Service Fabric uygulaması sürümleri** adım oluşturma.  Varsayılan olarak, bu derleme adımı hello yapı numarası tooall sürüm hello uygulama paketin bildirim dosyalarında değerler ekler. Merhaba bkz [görev belge sayfasının](https://go.microsoft.com/fwlink/?LinkId=820529) daha fazla bilgi için. Bu, her bir yükseltme dağıtımı hello önceki dağıtımından farklı sürüm değerleri gerektirdiğinden, uygulamanızın yükseltme desteklemek için yararlıdır. Toouse uygulama yükseltme iş akışınızda amaçlanmıyorsa, bu derleme adımı devre dışı bırakma düşünebilirsiniz. Tooproduce kullanılan toooverwrite var olan bir Service Fabric uygulaması olabilir bir yapı istiyorsanız devre dışı bırakılmalıdır. Merhaba yapı tarafından üretilen hello uygulamanın Hello sürümü hello uygulamanın hello kümedeki hello sürümü eşleşmiyorsa hello dağıtımı başarısız olur.
4. Çözümünüzü .NET Core proje içeriyorsa, yapı tanımınızı hello bağımlılıkları yükler bir derleme adımı içerdiğinden emin olun gerekir:
   1. Seçin **derleme adımı Ekle...** .
   2. Merhaba bulun **komut satırı** hello yardımcı programı sekmede görev ve onun Ekle düğmesini tıklatın.
   3. Merhaba görevin giriş alanları için değerleri aşağıdaki hello kullanın:
   4. Aracı: dotnet
   5. Bağımsız değişkenler: geri yükleme
   6. Hemen sonra hello olmasını hello görev sürükleyin **NuGet restore** adım.
5. Değişiklikleri toohello derleme tanımı yaptınız.

### <a name="try-it"></a>Deneyin
Seçin **Yapıyı Sıraya Al** toomanually bir yapı başlatın. Ayrıca Tetikleyiciler İtme veya iade oluşturur. Merhaba yapı başarıyla yürütüyor doğruladıktan sonra uygulama tooa kümenizi dağıtan bir yayın tanımı üzerinde toodefining şimdi taşıyabilirsiniz.

## <a name="create-a-release-definition"></a>Bir yayın tanımı oluşturun
Bir Team Services sürüm tanımı sırayla yürütülen görevler kümesinden oluşan bir iş akışını açıklar. Oluşturmakta olduğunuz hello yayın tanımı Hello amacı tootake bir uygulama paketidir ve tooa küme dağıtın. Birlikte kullanıldığında, hello yapı tanımı ve yayın tanımı kümenizde çalışan bir uygulama ile kaynak dosyaları tooending ile başlayan hello tüm iş akışı çalıştırabilirsiniz. Team Services hakkında daha fazla bilgi [yayın tanımları](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).

### <a name="create-a-definition-from-hello-release-template"></a>Merhaba yayın şablonundan bir tanımı oluşturun
1. Projenizi Visual Studio Team Services içinde açın.
2. Select hello **sürüm** sekmesi.
3. Select hello yeşil  **+**  toocreate yeni bir sürüm tanımı oturum ve seçin **oluşturma yayın tanımı** hello menüsünde.
4. Açılır hello iletişim kutusunda seçin **Azure Service Fabric dağıtımı** hello içinde **dağıtım** şablon kategorisi.
5. Seçin **sonraki**.
6. Bu sürüm tanımı hello kaynağı olarak toouse istediğiniz hello derleme tanımı'nı seçin.  Seçili hello tarafından üretilmiş olan hello yayın tanımı başvuruları hello yapıların yapı tanımı.
7. Merhaba denetleyin **sürekli dağıtım** toohave istiyorsanız kutuyu Team Services otomatik olarak yeni bir sürüm oluşturma ve her bir yapı tamamlandıktan Merhaba Service Fabric uygulaması dağıtma.
8. Merhaba aracı sıra toouse istediğiniz seçin. Barındırılan aracılar desteklenir.
9. **Oluştur**’u seçin.
10. Merhaba sayfanın üst kısmındaki hello hello kalem simgesine tıklayarak Hello tanımı adını düzenleyin.
11. Uygulamanızı dağıtılmalıdır hello küme toowhich hello seçin **küme bağlantısı** hello görevinin giriş alanı. Merhaba küme bağlantı hello dağıtım görev tooconnect toohello küme tanıyan hello gerekli bilgileri sağlar. Bir küme bağlantısı kümeniz için henüz yoksa, hello seçin **Yönet** köprü sonraki toohello alan tooadd biri. Açılır hello sayfasında hello aşağıdaki adımları gerçekleştirin:
    1. Seçin **yeni hizmet uç noktası** ve ardından **Azure Service Fabric** hello menüsünde.
    2. Merhaba bu bitiş noktası tarafından hedeflenen hello küme tarafından kullanılan kimlik doğrulama türünü seçin.
    3. Bağlantınız için bir ad hello tanımlayın **bağlantı adı** alan.  Genellikle, kümenizi hello adını kullanırsınız.
    4. Merhaba istemci bağlantı uç noktasının URL'sini hello tanımlamak **küme uç noktası** alan.  Örnek: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. Azure Active Directory kimlik bilgileri için toouse tooconnect toohello hello kümesinde istediğiniz hello bilgilerini tanımlayın **kullanıcıadı** ve **parola** alanları.
    6. Sertifika tabanlı kimlik doğrulaması için dosyasının hello istemci sertifikası hello hello Base64 kodlaması tanımlamak **istemci sertifikası** alan.  Merhaba Yardım açılır nasıl ilişkin bilgi için bu alan bakın değer tooget.  Sertifikanız parola korumalıysa hello parolası hello tanımlamak **parola** alan.
    7. Yaptığınız değişiklikleri onaylamak **Tamam**. Geri tooyour gezinme sonra yayın tanımı, hello hello Yenile simgesine tıklayın **küme bağlantısı** alan toosee hello eklediğiniz uç noktası.
12. Merhaba yayın tanımını kaydedin.

> [!NOTE]
> Microsoft Accounts (örneğin, @hotmail.com veya @outlook.com) Azure Active Directory kimlik doğrulaması ile desteklenmez.
> 
> 

oluşturulan hello tanımı oluşur bir görev türü **Service Fabric uygulama dağıtımı**. Merhaba bkz [görev belge sayfasının](https://go.microsoft.com/fwlink/?LinkId=820528) bu görev hakkında daha fazla bilgi için.

### <a name="verify-hello-template-defaults"></a>Merhaba şablon Varsayılanları doğrulayın
1. Merhaba doğrulayın **yayımlama profili** hello giriş alanını **Service Fabric uygulaması dağıtma** görev. Varsayılan olarak, bu alana hello yapı yapıtlarla birlikte bulunan Cloud.xml adlı bir yayımlama profili başvurur. Tooreference farklı yayımlama profili istiyorsanız ya da hello yapı yapılarının birden çok uygulama paketlerinde içeriyorsa, tooupdate hello yolunu uygun şekilde gerekir.
2. Merhaba doğrulayın **uygulama paketi** hello giriş alanını **Service Fabric uygulaması dağıtma** görev. Varsayılan olarak, bu alana hello varsayılan uygulama paket yolu hello derleme tanımı şablonda kullanılan başvurur.  Merhaba varsayılan uygulama paket yolu değiştirdiyseniz hello yapı tanımı, tooupdate hello yolunu uygun şekilde burada da gerekir.

### <a name="try-it"></a>Deneyin
Seçin **oluşturma yayın** hello gelen **yayın** düğmesi menü toomanually bir yayın oluşturun. Açılır hello iletişim kutusunda, toobase hello yayın istiyor ve ardından hello derleme seçme **oluşturma**. Sürekli dağıtım etkinleştirilirse, ilişkili hello derleme tanımı bir yapı tamamlandığında sürümleri otomatik olarak oluşturulur.

## <a name="next-steps"></a>Sonraki adımlar
toolearn makaleler hello okuma Service Fabric uygulamalarla sürekli tümleştirme hakkında daha fazla bilgi:

* [Team Services belgelerine giriş](https://www.visualstudio.com/docs/overview)
* [Yapılandırma yönetimi Team Services](https://www.visualstudio.com/docs/build/overview)
* [Yayın Yönetimi Team Services](https://www.visualstudio.com/docs/release/overview)

