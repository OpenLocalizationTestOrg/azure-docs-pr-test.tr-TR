---
title: "aaaPrepare toopublish veya Visual Studio'dan Azure bir uygulamayı dağıtma | Microsoft Docs"
description: "Azure uygulamanızı yapılandırmak ve Bulut ve depolama hesabı hizmetlerini Hello yordamları tooset öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>TooPublish hazırlayın veya Visual Studio'da bir Azure uygulama dağıtma
## <a name="overview"></a>Genel Bakış
Bir bulut hizmeti projesini yayımlamadan önce aşağıdaki hizmetleri hello ayarlamanız gerekir:

* A **bulut hizmeti** toorun hello Azure ortamı, rolleri
* A **depolama hesabı** toohello Blob, kuyruk ve tablo hizmetlerine erişim sağlar.

Uygulamanızı yapılandırmak ve bu hizmetleri yukarı yordamları tooset aşağıdaki hello kullanın

## <a name="create-a-cloud-service"></a>Bulut hizmeti oluşturun
bir bulut hizmeti tooAzure toopublish rollerinizi hello Azure ortamı çalıştıran bir bulut hizmeti önce oluşturmanız gerekir. Hello bir bulut hizmeti oluşturabilir [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885)hello bölümünde açıklandığı gibi **toocreate kullanarak bir bulut hizmeti hello Klasik Azure portalı**, bu konunun devamındaki. Bir bulut hizmeti Visual Studio'da yayımlama hello Sihirbazı'nı kullanarak da oluşturabilirsiniz.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate Visual Studio'yu kullanarak bir bulut hizmeti
1. Hello Azure projesi için hello kısayol menüsünü açın ve seçin **Yayımla**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Olarak oturum yapmadıysanız, oturum, kullanıcı adı ve parolayla hello Microsoft hesabı veya Azure aboneliğinizle ilişkili kuruluş hesabı için.
3. Merhaba seçin **sonraki** düğmesini tooadvance toohello **ayarları** sayfası.

    ![Yayımlama Sihirbazı ortak ayarları](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. Merhaba, **bulut Hizmetleri** listesinde, seçin **Yeni Oluştur**. Merhaba **Azure hizmetleri oluşturmak** iletişim kutusu görüntülenir.
5. Merhaba, bulut hizmetinizin adını girin. Merhaba adı hizmetiniz için hello URL parçası oluşturur ve bu nedenle genel olarak benzersiz olmalıdır. Merhaba adı büyük küçük harfe duyarlı değil.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalı kullanarak bir bulut hizmeti
1. İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkId=253103) hello Microsoft Web sitesinde.
2. (isteğe bağlı) toodisplay önceden oluşturduğunuz, bulut hizmetlerinin listesi hello sayfasının sol tarafında hello hello bulut Hizmetleri bağlantısını seçin.
3. Merhaba seçin  **+**  sol alt hello simgesinde köşe ve ardından **bulut hizmeti** hello menüsünde görüntülenir. İki seçenek, başka bir ekran **hızlı Oluştur** ve **özel Oluştur**, görüntülenir. Seçerseniz **hızlı Oluştur**, burada, fiziksel olarak barındırılacağı, URL ve hello bölge belirterek bir bulut hizmeti oluşturabilir. Seçerseniz **özel Oluştur**, bir paketi (.cspkg dosyası), bir yapılandırma (.cscfg) dosyası ve bir sertifika belirterek, bir bulut hizmeti hemen yayımlayabilirsiniz. Hello kullanarak bulut hizmetiniz toopublish düşünüyorsanız, özel Oluştur gerekli değil **Yayımla** Azure projesinde komutu. Merhaba **Yayımla** komutu hello kısayol menüsünde bir Azure projesi için kullanılabilir.
4. Seçin **hızlı Oluştur** toolater Visual Studio kullanarak bulut hizmetinizi yayımlayın.
5. Bulut hizmetiniz için bir ad belirtin. Merhaba tam URL sonraki toohello adı görüntülenir.
6. Merhaba listesinde, kullanıcılarınızın çoğu bulunduğu hello bölgeyi seçin.
7. Merhaba hello penceresinin Hello altında seçin **bulut hizmeti oluşturma** bağlantı.

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma
Bir depolama hesabı toohello Blob, kuyruk ve tablo hizmetlerine erişim sağlar. Visual Studio veya hello kullanarak bir depolama hesabı oluşturabilirsiniz [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate Visual Studio kullanarak bir depolama hesabı
1. İçinde **Çözüm Gezgini**açın hello hello kısayol menüsünü **depolama** düğümünü ve ardından **depolama hesabı oluştur**.

    ![Yeni bir Azure depolama hesabı oluşturma](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Bilgi hello hello yeni depolama hesabı için aşağıdaki hello girin veya seçin **depolama hesabı oluştur** iletişim kutusu.

   * hello Azure aboneliği toowhich tooadd hello depolama hesabı istiyor.
   * Merhaba yeni depolama hesabı için toouse istediğiniz hello adı.
   * Merhaba bölge veya benzeşim grubunda (örneğin, Batı ABD veya Doğu Asya).
   * Merhaba türü çoğaltmasını coğrafi olarak yedekli gibi hello depolama hesabı için toouse istiyor.
3. İşiniz bittiğinde seçin **oluşturma**.hello yeni depolama hesabı görünür hello **depolama** listesinde **Sunucu Gezgini**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalı kullanarak bir depolama hesabı
1. İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkId=253103) hello Microsoft Web sitesinde.
2. (İsteğe bağlı) tooview, depolama hesaplarını seçme hello **depolama** hello hello yan hello sayfasının sol panelde bağlantıyı.
3. Merhaba sol alt köşedeki hello sayfasının, hello seçin  **+**  simgesi.
4. Görüntülenen başlangıç menüsünde seçin **depolama**ve ardından **hızlı Oluştur**.
5. Merhaba depolama hesabı benzersiz bir url neden olacak bir ad verin.
6. Bulut hizmetiniz bir ad verin. Merhaba tam URL sonraki toohello adı görüntülenir.
7. Bölgeler Hello listede kullanıcılarınızın çoğu bulunduğu bir bölge seçin.
8. Tooenable coğrafi çoğaltma isteyip istemediğinizi belirtin. Coğrafi çoğaltma devre dışı bırakırsanız, verilerinizi birden çok fiziksel konumlara tooreduce hello kaybı olasılığı kaydedilir. Bu özellik depolama daha maliyetli hale getirir, ancak hello özelliği daha sonra eklemek yerine hello depolama hesabı oluşturduğunuzda, coğrafi konum sağlayarak hello maliyetini azaltabilir. Daha fazla bilgi için bkz: [coğrafi çoğaltma](http://go.microsoft.com/fwlink/?LinkId=253108).
9. Merhaba hello penceresinin Hello altında seçin **depolama hesabı oluştur** bağlantı.

Depolama hesabınızı oluşturduktan sonra her hello Azure storage Hizmetleri tooaccess kaynakları kullanın ve hesabınız için birincil ve ikincil erişim anahtarları da hello hello URL'leri görürsünüz. Bunları anahtarları hello depolama hizmetleri karşı yapılan tooauthenticate istekleri.

> [!NOTE]
> Merhaba ikincil erişim anahtarını aynı hello birincil erişim anahtarı olarak tooyour depolama hesabına erişim ve yedekleme olarak birincil erişim anahtarınız riske oluşturulur hello sağlar. Ayrıca, erişim anahtarlarınızı düzenli olarak yeniden önerilir. Merhaba birincil anahtarı yeniden oluşturmak hello ikincil anahtarı yeniden oluşturmak toouse yeniden hello birincil anahtar değiştirebilirsiniz bir bağlantı dizesi ayarı toouse hello ikincil anahtar değiştirebilirsiniz.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Merhaba depolama hesabı tarafından sağlanan uygulama toouse hizmetlerinizi yapılandırın
Oluşturduğunuz depolama hizmetleri toouse hello Azure storage Hizmetleri erişen herhangi bir rolü yapılandırmanız gerekir. toodo Bu, Azure projeniz için birden çok hizmet yapılandırması kullanabilirsiniz. Varsayılan olarak, iki Azure projenizde oluşturulur. Birden çok hizmet yapılandırması kullanarak, aynı bağlantı kodunuzda dize, ancak her hizmet yapılandırmasında bir bağlantı dizesi için farklı bir değere sahip hello kullanabilirsiniz. Örneğin, bir hizmet yapılandırması toorun kullanın ve uygulamanızı yerel olarak hello Azure storage öykünücüsü ve farklı hizmet yapılandırma toopublish kullanarak uygulama tooAzure hata ayıklama. Hizmet yapılandırması hakkında daha fazla bilgi için bkz: [yapılandırma bilgisayarınızı Azure projesi kullanarak birden çok hizmet yapılandırması](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>Depolama hesabı hello uygulama toouse hizmetlerinizi tooconfigure sağlar
1. Visual Studio'da Azure çözümünüzü açın. Çözüm Gezgini'nde hello depolama hizmetleri erişen Azure projenizde her rol için hello kısayol menüsünü açın ve seçin **özellikleri**. Merhaba Visual Studio düzenleyicisinde hello hello rolün adını içeren bir sayfa görüntülenir. başlangıç sayfasını görüntüler hello alanları hello için **yapılandırma** sekmesi.
2. Merhaba özellik sayfalarında hello rol için seçin **ayarları**.
3. Merhaba, **hizmet yapılandırmasını** listesinde, tooedit istediğiniz hello hizmet yapılandırmasını hello adını seçin. Bu rol için hello hizmet yapılandırmaların toomake değişiklikleri tooall istiyorsanız, seçebileceğiniz **tüm yapılandırmaları**.  Merhaba bölüm nasıl tooupdate hizmet yapılandırmaları hakkında daha fazla bilgi için bkz **depolama hesapları için bağlantı dizelerini Yönet** hello konudaki [hello rollerini Visual Studio ile Azure bulut hizmeti için yapılandırma ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify herhangi bir bağlantı dizesi ayarlarının seçin hello **...** Düğme sonraki toohello ayar. Merhaba **depolama bağlantı dizesi oluştur** iletişim kutusu görüntülenir.
5. Altında **bağlanırken**, hello seçin **aboneliğinizi** seçeneği.
6. Merhaba, **abonelik** listesinde, aboneliğinizi seçin. Aboneliklerin listesini Hello hello istediğiniz içermiyorsa, hello seçin **yayımlama ayarları indirme** bağlantı.
7. Merhaba, **hesap adı** listesinde, depolama hesabınızın adını seçin. Azure Araçları edinir depolama hesabının kimlik bilgilerini otomatik olarak hello .publishsettings dosyasını kullanarak. Depolama hesabınızın kimlik bilgileri el ile toospecify seçin hello **kimlik bilgileri'el ile girilen** seçeneğini ve ardından bu yordama devam edin. Depolama hesabı adı ve birincil anahtar hello alabilirsiniz [Klasik Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885). Toospecify istemiyorsanız, depolama hesabı ayarlarını el ile Merhaba seçin **Tamam** düğmesini tooclose hello iletişim kutusu.
8. Merhaba seçin **depolama hesabını girin** kimlik bilgileri bağlantı.
9. Merhaba, **hesap adı** kutusuna, hello depolama hesabınızın adını girin.

   > [!NOTE]
   > Merhaba günlüğüne [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885)ve ardından hello **depolama** düğmesi. Merhaba portal depolama hesaplarının listesini gösterir. Bir hesap seçerseniz, onun için bir sayfa açar. Bu sayfadan hello hello depolama hesabının adını kopyalayabilirsiniz. Merhaba Klasik portal önceki bir sürümünü kullanıyorsanız, depolama hesabınızın adını hello hello görünür **depolama hesapları** görünümü. toocopy bu ad, hello Vurgula **özellikleri** bu pencereyi görüntülemek ve hello Ctrl-C tuş'u seçin. Visual Studio uygulamasına toopaste hello adı seçin hello **hesap adı** metin kutusuna ve ardından hello Ctrl + V tuşlarını seçin.
   >
   >
10. Merhaba, **hesap anahtarı** kutusunda, birincil anahtarınızı girin veya kopyalayın ve hello yapıştırın [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
     Bu anahtar toocopy:

    1. Merhaba hello uygun depolama hesabı için başlangıç sayfasının Hello altında seçin **anahtarları Yönet** düğmesi.
    2. Merhaba üzerinde **anahtarları erişimi Yönet** sayfasında hello birincil erişim anahtarını hello metnini seçin ve hello Ctrl + C tuş'u seçin.
    3. Azure Araçları'nda, hello anahtar hello yapıştırma **hesap anahtarı** kutusu.
    4. Aşağıdaki seçenekler toodetermine hello birini seçmeniz gerekir nasıl hello hizmet hello depolama hesabı erişim sağlar:

       * **HTTP kullanmak**. Merhaba standart seçenek budur. Örneğin, `http://<account name>.blob.core.windows.net`.
       * **HTTPS kullanmak** güvenli bir bağlantı için. Örneğin, `https://<accountname>.blob.core.windows.net`.
       * **Özel uç noktaları belirtin** hello üç hizmetlerinin her biri için. Bu uç noktalar, hello belirli hizmet hello alanına sonra yazabilirsiniz.

         > [!NOTE]
         > Özel uç noktaları oluşturursanız, daha karmaşık bir bağlantı dizesi oluşturabilirsiniz. Bu dize biçimi kullandığınızda, depolama hesabınıza hello Blob hizmeti ile kaydettiğiniz bir özel etki alanı adını içeren Depolama Hizmeti uç noktaları belirtebilirsiniz. Aynı zamanda yalnızca tek bir kapsayıcı paylaşılan erişim imzası aracılığıyla tooblob kaynaklara erişim izni verebilir. Hakkında daha fazla bilgi için bkz toocreate özel uç noktaları, [Azure Storage bağlantı dizelerini yapılandırma](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave Bu bağlantı dizesi değişiklikler seçin hello **Tamam** düğmesine ve ardından hello **kaydetmek** hello araç çubuğunda. Bu değişiklikleri kaydettikten sonra bu bağlantı dizesi hello değerini kodunuzda kullanarak alabileceğiniz [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Uygulama tooAzure yayımladığınızda, hello bağlantı dizesi için hello Azure depolama hesabını içeren hello hizmet yapılandırması seçin. Uygulamanızı yayımlandıktan sonra Merhaba uygulaması hello Azure storage hizmetlerine karşı beklendiği gibi çalıştığını doğrulayın

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio'dan uygulamaları tooAzure yayımlama hakkında daha fazla toolearn bkz [yayımlama hello Azure araçlarını kullanarak bir bulut hizmeti](vs-azure-tools-publishing-a-cloud-service.md).
