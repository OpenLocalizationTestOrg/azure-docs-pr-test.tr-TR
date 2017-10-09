---
title: "aaaHow toomanage hizmet yapılandırmalarını ve profilleri | Microsoft Docs"
description: "Bilgi nasıl hizmet yapılandırmalarını ve profilleri yapılandırma dosyalarını toowork | hangi hello dağıtım ortamları için ayarları depolar ve bulut Hizmetleri için yayınlama ayarlarını."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>Toomanage nasıl hizmet yapılandırmalarını ve profilleri
## <a name="overview"></a>Genel Bakış
Bir bulut hizmeti yayımladığınızda, Visual Studio yapılandırma dosyaları iki tür yapılandırma bilgileri depolar: hizmet yapılandırmalarını ve Profiller. Hizmet yapılandırması (.cscfg dosyaları) hello dağıtım ortamları için bir Azure bulut hizmeti için ayarları depolar. Azure bulut hizmetlerinizi yönetir bu yapılandırma dosyalarını kullanır. Üzerindeki diğer yandan Merhaba, profilleri (.azurePubxml dosyaları) deposu için yayımlama ayarları bulut Hizmetleri. Bu, hello kullandığınızda, seçtiğiniz kaydını Yayımlama Sihirbazı ve yerel olarak Visual Studio tarafından kullanılan ayarlardır. Bu konuda açıklanmaktadır nasıl toowork yapılandırma dosyaları her iki tür.

## <a name="service-configurations"></a>Hizmet yapılandırması
Her dağıtım ortamınız için birden çok hizmet yapılandırmaları toouse oluşturabilirsiniz. Örneğin, bir hizmet yapılandırması toorun kullanın ve Azure uygulaması ve başka bir hizmet yapılandırması, üretim ortamınız için test hello yerel ortam oluşturabilirsiniz.

Ekleme, silme, yeniden adlandırın ve gereksinimlerinize göre bu hizmet yapılandırması değiştirme. Hello aşağıdaki çizimde gösterildiği gibi bu hizmet yapılandırması Visual Studio'dan yönetebilirsiniz.

![Hizmet yapılandırmalarını Yönet](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

Merhaba da açabilirsiniz **yönetmek yapılandırmaları** hello rolün özellik sayfaları iletişim kutusu. Azure projenizdeki bir rol için tooopen hello özellikleri bu rol için hello kısayol menüsünü açın ve ardından **özellikleri**. Merhaba üzerinde **ayarları** sekmesinde, hello genişletin **hizmet yapılandırmasını** listeleyin ve ardından **Yönet** tooopen hello **yönetmek yapılandırmaları**iletişim kutusu.

### <a name="tooadd-a-service-configuration"></a>tooadd bir hizmet yapılandırması
1. Çözüm Gezgini'nde hello Azure projesi için hello kısayol menüsünü açın ve ardından **yönetmek yapılandırmaları**.
   
    Merhaba **hizmet yapılandırmalarını Yönet** iletişim kutusu görüntülenir.
2. tooadd bir hizmet yapılandırması, varolan bir yapılandırma bir kopyasını oluşturmanız gerekir. toodo bunu toocopy hello adı listesinden istediğiniz ve ardından hello yapılandırması seçin **kopya oluştur**.
3. (İsteğe bağlı) toogive hello hizmet yapılandırması farklı bir ad hello yeni hizmet yapılandırması hello adı listesinden seçin ve ardından **yeniden adlandırma**. Merhaba, **adı** metin kutusunda, bu hizmet yapılandırması toouse istediğiniz ve ardından türü hello adı **Tamam**.
   
    ServiceConfiguration adlı yeni bir hizmet yapılandırma dosyası. [Yeni adı] .cscfg, Çözüm Gezgini'nde toohello Azure projesi eklenir.

### <a name="toodelete-a-service-configuration"></a>toodelete bir hizmet yapılandırması
1. Çözüm Gezgini'nde hello Azure projesi için hello kısayol menüsünü açın ve ardından **yönetmek yapılandırmaları**.
   
    Merhaba **hizmet yapılandırmalarını Yönet** iletişim kutusu görüntülenir.
2. toodelete bir hizmet yapılandırması seçin hello yapılandırma hello gelen toodelete istediğiniz **adı** listeleyin ve ardından **kaldırmak**. Bu yapılandırma toodelete istediğiniz tooverify bir iletişim kutusu görüntülenir.
3. **Sil**’i seçin.
   
     Merhaba hizmet yapılandırma dosyası hello Azure projesi Çözüm Gezgini'nde kaldırılır.

### <a name="toorename-a-service-configuration"></a>toorename bir hizmet yapılandırması
1. Çözüm Gezgini'nde, hello Azure projesi için hello kısayol menüsünü açın ve ardından **yönetmek yapılandırmaları**.
   
    Merhaba **hizmet yapılandırmalarını Yönet** iletişim kutusu görüntülenir.
2. toorename bir hizmet yapılandırması seçin hello yeni hizmet yapılandırması hello **adı** listeleyin ve ardından **yeniden adlandırma**. Merhaba, **adı** metin kutusunda, bu hizmet yapılandırması toouse istediğiniz ve ardından türü hello adı **Tamam**.
   
    Merhaba hello hizmet yapılandırma dosyasının adını, Çözüm Gezgini'nde Azure projesi hello değiştirilir.

### <a name="toochange-a-service-configuration"></a>toochange bir hizmet yapılandırması
* Toochange bir hizmet yapılandırması istiyorsanız hello Azure projesi toochange istediğiniz ve ardından hello belirli rol için hello kısayol menüsünü açın **özellikleri**. Bkz: [nasıl yapılır: Visual Studio ile Azure bulut hizmeti için hello rollerini yapılandırma](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) daha fazla bilgi için.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Profilleri kullanılarak farklı ayar birleşimleri olun
Bir profil kullanarak hello otomatik olarak doldurabilir **Yayımlama Sihirbazı** farklı amaçlar için ayarları farklı bileşimleri ile. Örneğin, hata ayıklama için bir profil olabilir ve yayın için başka bir oluşturur. Bu durumda, **hata ayıklama** profil sahip olabilir **IntelliTrace** etkin ve hello **hata ayıklama** seçili, yapılandırma ve **sürüm** Profil sahip olabilir **IntelliTrace** devre dışı bırakılır ve hello **sürüm** seçili yapılandırma. Farklı bir depolama hesabı kullanarak bir hizmet farklı profiller toodeploy de kullanabilirsiniz.

Merhaba hello Sihirbazı ilk kez çalıştırdığınızda, bir varsayılan profili oluşturulur. Visual Studio hello profil tooyour hello altında Azure projesi eklenir .azurePubXml uzantısına sahip bir dosyada depolar **profilleri** klasör. Daha sonra hello Sihirbazı'nı çalıştırdığınızda, el ile farklı seçenekler belirtirseniz, hello dosya otomatik olarak güncelleştirir. Aşağıdaki yordamı hello çalıştırmadan önce önceden bulut hizmetiniz en az bir kez yayımladığınız.

### <a name="tooadd-a-profile"></a>tooadd bir profili
1. Azure projeniz için hello kısayol menüsünü açın ve ardından **Yayımla**.
2. Sonraki toohello **hedef profil** listesi, select hello **profili Kaydet** düğme, aşağıdaki çizimde gösterildiği hello olarak. Bu profil sizin için oluşturur.
   
    ![Yeni bir profil oluşturma](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Hello profil oluşturulduktan sonra seçin **< Yönet... >** hello içinde **hedef profil** listesi.
   
    Merhaba **profillerini yönetme** iletişim kutusu görüntülenirse, aşağıdaki çizimde gösterildiği hello.
   
    ![Profilleri Yönet iletişim kutusu](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. Merhaba, **adı** listesinde, bir profil seçin ve ardından **kopya oluştur**.
5. Merhaba seçin **Kapat** düğmesi.
   
    Merhaba yeni profili hello hedef profil listesi görüntülenir.
6. Merhaba, **hedef profil** listesinde, oluşturduğunuz select hello profili. Merhaba Yayımlama Sihirbazı ayarları seçtiğiniz hello profili hello seçeneklerden doldurulur.
7. Select hello **önceki** ve **sonraki** toodisplay hello Yayımlama Sihirbazı'nı her sayfanın düğmeler ve ardından bu profil için hello ayarlarını özelleştirin. Bkz: [Azure uygulaması Yayımlama Sihirbazı](http://go.microsoft.com/fwlink/p/?LinkID=623085) bilgi.
8. Hello ayarlarını özelleştirme tamamladıktan sonra Seç **sonraki** toogo geri toohello Ayarları sayfası. Bu ayarları kullanarak hello hizmet yayımladığınızda veya seçerseniz Hello profili kaydedildi **kaydetmek** profilleri sonraki toohello listesi.

### <a name="toorename-or-delete-a-profile"></a>toorename veya bir profili silme
1. Azure projeniz için hello kısayol menüsünü açın ve ardından **Yayımla**.
2. Merhaba, **hedef profil** listesinde **Yönet**.
3. Merhaba, **profillerini yönetme** iletişim kutusu, toodelete istediğiniz ve ardından select hello profil **kaldırmak**.
4. Görüntülenen hello onay iletişim kutusunda **Tamam**.
5. Seçin **Kapat**.

### <a name="toochange-a-profile"></a>toochange bir profili
1. Azure projeniz için hello kısayol menüsünü açın ve ardından **Yayımla**.
2. Merhaba, **hedef profil** listesinde, select hello profil toochange istiyor.
3. Select hello **önceki** ve **sonraki** toodisplay her sayfanın hello Yayımlama Sihirbazı'nı ve ardından istediğiniz hello ayarlarını değiştir düğmeleri. Bkz: [Azure uygulaması Yayımlama Sihirbazı](http://go.microsoft.com/fwlink/p/?LinkID=623085) bilgi.
4. Hello ayarlarını değiştirme işlemini tamamladıktan sonra seçin **sonraki** toogo geri toohello **ayarları** sayfası.
5. (İsteğe bağlı) seçin **Yayımla** hello yeni ayarlarla toopublish hello bulut hizmeti. Bulut hizmetiniz bu saat ve Kapat toopublish istemiyorsanız, Yayımlama Sihirbazı Merhaba, Visual Studio toosave hello değişiklikleri toohello profili isteyip istemediğinizi sorar.

## <a name="next-steps"></a>Sonraki adımlar
diğer Azure projeniz Visual Studio'dan bölümlerini yapılandırma hakkında daha fazla toolearn bakın [bir Azure projesi yapılandırma](http://go.microsoft.com/fwlink/p/?LinkID=623075)

