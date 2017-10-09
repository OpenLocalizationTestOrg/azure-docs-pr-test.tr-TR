---
title: "aaaPublishing hello Azure araçlarını kullanarak bir bulut hizmeti | Microsoft Docs"
description: "Nasıl toopublish Azure bulut hizmeti projeleri Visual Studio kullanarak hakkında bilgi edinin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Yayımlama hello Azure araçlarını kullanarak bir bulut hizmeti
Microsoft Visual Studio için Hello Azure araçlarını kullanarak, Azure uygulamanızı Visual Studio'dan doğrudan yayımlayabilirsiniz. Tümleşik visual Studio destekler tooeither yayımlama hello hazırlama veya üretim ortamında bir bulut hizmeti hello.

Azure bir uygulamayı yayımlamadan önce bir Azure aboneliğinizin olması gerekir. Uygulamanız tarafından kullanılan bir bulut hizmeti ve depolama hesabı toobe da ayarlamanız gerekir. Bunlar hello ayarlayabilirsiniz [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Yayımladığınızda, bulut hizmetinizin hello dağıtım ortamı seçebilirsiniz. Ayrıca kullanılan toostore hello uygulama paketi dağıtım için bir depolama hesabı seçmeniz gerekir. Dağıtımdan sonra hello uygulama paketi hello depolama hesabından kaldırılır.
> 
> 

Geliştirme ve Azure uygulamanızı test ederken, Web dağıtımı toopublish değişiklikleri web rolleri için artımlı olarak kullanabilirsiniz. Uygulama tooa dağıtım ortamınızı yayımladıktan sonra Web dağıtımı hello web rolü çalıştıran toohello sanal makine doğrudan değişiklikleri dağıtmanıza olanak tanır. Değil toopackage olması ve tüm Azure alt uygulamanız, web rolü tootest hello değişiklikleri çıkışı tooupdate istediğiniz her zaman yayımlayın. Bu yaklaşımda, uygulama yayımlanan tooa dağıtım ortamınızı bekleme toohave test hello bulutta web rolü değişikliklerinizi kullanılabilir olabilir.

Yordamları toopublish aşağıdaki Merhaba, Web dağıtımı kullanarak Azure uygulaması ve web rolü tooupdate kullanın:

* Yayımlama veya Visual Studio'dan Azure bir uygulama paketi
* Bir web rolü hello geliştirme ve Test döngüsünün parçası olarak güncelleştirme

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Yayımlama veya Visual Studio'dan Azure bir uygulama paketi
Azure uygulamanızı yayımladığınızda, görevleri aşağıdaki hello birini yapabilirsiniz:

* Bir hizmet paketi oluşturun: Bu paket ve hello hizmet yapılandırma dosyası toopublish uygulama tooa dağıtım ortamınızdan hello kullanabilirsiniz [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
* Visual Studio'dan Azure projenizi yayımlayın: toopublish uygulamanız tooAzure, kullandığınız doğrudan hello Yayımlama Sihirbazı. Bilgi için bkz: [Azure uygulaması Yayımlama Sihirbazı](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate Visual Studio'dan bir hizmet paketi
1. Hazır toopublish olduğunda, uygulamanızın Çözüm Gezgini'nde, Merhaba, rollerinizi içeren Azure projesi için açık hello kısayol menüsünü açın ve Yayımla seçin.
2. bir hizmet paketi toocreate yalnızca, şu adımları izleyin:  
   
   1. Merhaba kısayol menüsünde hello Azure projesi, seçin **paket**.
   2. Merhaba, **paket Azure uygulama** iletişim kutusunda, hello hizmet yapılandırmasını toocreate istediğiniz paketi seçin ve hello yapı yapılandırması seçin.
   3. Uzak Masaüstü (isteğe bağlı) tooturn, select hello yayımladıktan sonra hello bulut hizmeti için **tüm roller için Uzak Masaüstü'yi etkinleştirmek** onay kutusunu işaretleyin ve ardından **ayarları** tooconfigure Uzak Masaüstü. Yayımladıktan sonra bulut hizmetinizin toodebug istiyorsanız, uzak seçerek hata ayıklama etkinleştirme **etkinleştirmek uzaktan hata ayıklayıcı tüm rolleri için**.
      
      Daha fazla bilgi için bkz: [Azure rolleri ile Uzak Masaüstü kullanarak](vs-azure-tools-remote-desktop-roles.md).
   4. toocreate hello paketini, hello seçin **paket** bağlantı.
      
      Dosya Gezgini Yeni paket oluşturulan hello hello dosya konumu gösterir. Böylece hello kullanabilirsiniz, bu konuma kopyalayabilirsiniz [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish bu paketi tooa dağıtım ortamı bir bulut hizmeti oluşturup bu hello paket tooan ortamıyla dağıttığınızda paket konumu hello olarak bu konum kullanmalısınız [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
3. (İsteğe bağlı) toocancel hello dağıtım işlemi, hello satır öğenin hello etkinlik günlüğü ' nde hello kısayol menüsünde seçin **iptal et ve Kaldır**. Bu hello dağıtım işlemi durdurur ve Azure'dan hello dağıtım ortamı siler.
   
   > [!NOTE]
   > Bu dağıtım ortamı sonraki tooremove süredir dağıtıldı, hello kullanmalısınız [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (İsteğe bağlı) Rolü örneklerinizi başlattıktan sonra Visual Studio hello dağıtım ortamı hello otomatik olarak gösterir. **bulut Hizmetleri** Sunucu Gezgininde. Buradan, hello tek rol örneklerini hello durumunu görebilirsiniz. Bkz: [bulut Gezgini ile yönetme Azure kaynaklarını](vs-azure-tools-resources-managing-with-cloud-explorer.md)çizim aşağıdaki .hello hala hello başlatılıyor durumu durumdayken hello rol örnekleri gösterir:
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Bir Web rolü parçası hello geliştirme ve test döngüsü olarak güncelleştirme
Uygulamanızın arka uç altyapısı kararlı olduğundan, ancak hello web rolleri daha sık sık güncelleştirilmesi gerekmeyen, Web dağıtımı tooupdate yalnızca bir web rolü projenizde kullanabilirsiniz. Bu, toorebuild istediğiniz yoksa ve hello arka uç çalışan rolleri yeniden dağıtın veya birden çok web rolleri varsa ve tooupdate hello web rolleri yalnızca biri istiyorsanız kullanışlıdır.

### <a name="requirements"></a>Gereksinimler
Web rolünüz hello gereksinimleri toouse Web dağıtımı tooupdate şunlardır:

* **Geliştirme ve sınama amacıyla yalnızca:** hello değişiklik yapıldıysa doğrudan toohello sanal makine hello web rolü çalıştığı. Bu sanal makine geri dönüşüm toobe varsa, yayımladığınız hello özgün paket hello rol için kullanılan toorecreate hello sanal makine olduğundan hello değişiklikler kaybolur. Uygulama tooget hello son değişiklikleri hello web rolü için yeniden yayımlamanız gerekir.
* **Yalnızca web rolleri güncelleştirilebilir:** çalışan rolleri güncelleştirilemez. Ayrıca, web role.cs hello RoleEntryPoint güncelleştirilemiyor.
* **Web rolü tek bir örneği yalnızca destekleyebilir:** dağıtım ortamınızda herhangi bir web rolü birden fazla örneğini içeremez. Ancak, birden çok web rolleri her yalnızca bir örneği ile desteklenir.
* **Uzak Masaüstü bağlantılarını etkinleştirmeniz gerekir:** Web dağıtımı hello kullanıcı ve Internet Information Services (IIS) çalıştıran parola tooconnect toohello sanal makine toodeploy hello değişiklikleri toohello sunucu kullanabilmesi için bu gereklidir. Ayrıca, tooconnect toohello sanal makine tooadd bu sanal makinede bir güvenilen sertifika tooIIS gerekebilir. (Bu hello uzak bağlantı Web dağıtımı tarafından kullanılan bir IIS güvenli olmasını sağlar.)

Merhaba aşağıdaki yordamı hello kullandığınızı varsayar **Azure uygulamasını Yayımla** Sihirbazı.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable Web olduğunda, yayımlama uygulamanızı dağıtmak
1. tooenable hello **Web dağıtımını etkinleştirin** tüm rolleri onay kutusunu web için Uzak Masaüstü bağlantıları ilk yapılandırmanız gerekir. Seçin **Uzak Masaüstü'nü etkinleştirme** tüm rolleri ve ardından uzaktan hello içinde kullanılan tooconnect olacak tedarik hello kimlik bilgileri için **uzak masaüstü yapılandırması** görüntülenen kutusunda. Bkz: [Azure rolleri ile Uzak Masaüstü kullanarak](vs-azure-tools-remote-desktop-roles.md) daha fazla bilgi için.
2. tüm web rolleri, uygulamanızda hello tooenable Web dağıtımı seçin **tüm web rolleri için Web dağıtımını etkinleştirin**.
   
    Sarı bir uyarı üçgen görünür. Web dağıtımı hassas verileri yüklemek için önerilmez varsayılan olarak, güvenilmeyen, kendinden imzalı bir sertifika kullanır. Bu işlem için hassas verileri toosecure ihtiyacınız varsa, Web dağıtımı bağlantıları için kullanılan bir SSL sertifikası toobe ekleyebilirsiniz. Bu sertifikanın toobe güvenilen bir sertifika gerekir. Hakkında bilgi için toodo bunu hello bölümüne bakın **tooMake dağıtmak güvenli Web** bu konuda daha sonra.
3. Seçin **sonraki** tooshow hello **Özet** ekran ve ardından **Yayımla** toodeploy hello bulut hizmeti.
   
    Merhaba bulut hizmeti yayımlanır. oluşturulan Hello sanal makine yeniden yayımlanması olmadan web rolleri Web dağıtımı kullanılan tooupdate olabilmesi için IIS etkin Uzak bağlantıları vardır.
   
   > [!NOTE]
   > Web rolü için yapılandırılmış birden fazla örneği varsa, her web rolü toopublish uygulamanızın oluşturduğu hello paket sınırlı tooone örneğinde olacağını belirten bir uyarı iletisi görüntülenir. Seçin **Tamam** toocontinue. Hello gereksinimleri bölümünde belirtildiği gibi bir web rolü ancak her bir rolü yalnızca bir örneğine birden fazla olabilir.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate kullanarak Web dağıtımı tarafından bilgisayarınızı Web rolü
1. toouse Web dağıtımı, kod değişiklikleri toohello projesi için web rollerinin herhangi birinde, toopublish, istediğiniz çözümünüzde bu proje düğümüne sağ tıklayın ve çok noktası, Visual Studio olun**Yayımla**. Merhaba **Web'i Yayımla** iletişim kutusu görüntülenir.
2. (İsteğe bağlı) IIS için Uzak bağlantılar için güvenilir bir SSL sertifikası toouse eklediyseniz, hello temizleyebilirsiniz **izin Güvenilmeyen sertifika** onay kutusu. Merhaba bölüm tooadd sertifika toomake Web dağıtımı güvenliğini nasıl hakkında daha fazla bilgi için bkz **tooMake Web dağıtımı güvenli** bu konuda daha sonra.
3. toouse Web dağıtımı, hello mekanizması yayımlama hello kullanıcı adı ve hello paketi ilk kez yayımlandığında ayarladığınız, Uzak Masaüstü bağlantısı için parola gerekiyor.
   
   1. İçinde **kullanıcı adı**, hello kullanıcı adı girin.
   2. İçinde **parola**, hello parolayı girin.
   3. (İsteğe bağlı) Bu profildeki bu parolayı toosave istiyorsanız, tercih **Parolayı Kaydet**.
4. toopublish hello değişiklikleri tooyour web rolü seçin **Yayımla**.
   
    Merhaba durum satırı görüntüler **başlatılan Yayımla**. Yayımlama Hello tamamlandığında, **başarılı Yayımla** görüntülenir. Merhaba değişiklikleri şimdi dağıtılan toohello web rolü, sanal makinenizde olmuştur. Şimdi, Azure uygulamanız hello Azure ortamı tootest değişikliklerinizi başlatabilirsiniz.

### <a name="toomake-web-deploy-secure"></a>tooMake güvenli Web dağıtma
1. Web dağıtımı hassas verileri yüklemek için önerilmez varsayılan olarak, güvenilmeyen, kendinden imzalı bir sertifika kullanır. Bu işlem için hassas verileri toosecure ihtiyacınız varsa, Web dağıtımı bağlantıları için kullanılan bir SSL sertifikası toobe ekleyebilirsiniz. Bu sertifikanın toobe bir sertifika yetkilisinden (CA) elde güvenilen bir sertifika gerekir.
   
    toomake Web dağıtımı web rollerinin her biri için her bir sanal makine için güvenli, web dağıtımı için toohello toouse istediğiniz hello güvenilen sertifika karşıya gerekir [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885). Bu, uygulamanızın yayımladığınızda, hello web rolü için oluşturulan toohello sanal makine hello sertifikanın eklendiğinden emin hale getirir.
2. Uzak bağlantılar için güvenilir bir SSL sertifikası tooIIS toouse tooadd şu adımları izleyin:
   
   1. Merhaba web rolü, select hello örneğini hello web rolünde çalışan tooconnect toohello sanal makine **Cloud Explorer** veya **Sunucu Gezgini**ve ardından hello **kullanarak bağlan Uzak Masaüstü** komutu. Ayrıntılı adımlar için tooconnect toohello sanal makine, bkz: [Azure rolleri ile Uzak Masaüstü kullanarak](vs-azure-tools-remote-desktop-roles.md).
      
      Tarayıcınız toodownload ister bir. RDP dosyası.
   2. tooadd bir SSL sertifikası açık hello yönetim hizmeti IIS Yöneticisi'nde. IIS Yöneticisi'nde açma hello tarafından SSL'yi **bağlamaları** hello bağlantıyı **eylemi** bölmesi. Merhaba **Site bağlaması Ekle** iletişim kutusu görüntülenir. Seçin **Ekle**ve ardından HTTPS hello **türü** açılır liste. Merhaba, **SSL sertifikası** listesinde, hello SSL sertifikası bir CA tarafından imzalanmış ve toohello karşıya seçin [Klasik Azure portalı](http://go.microsoft.com/fwlink/?LinkID=213885). Daha fazla bilgi için bkz: [hello yönetim hizmeti için bağlantı ayarlarını yapılandır](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Güvenilir bir SSL sertifikası eklerseniz, hello sarı uyarı artık hello üçgen **Yayımlama Sihirbazı**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Merhaba hizmet paketi dosyaları dahil etme
Bir rol için oluşturulan hello sanal makinede kullanılabilir; böylece, hizmet paketinde tooinclude belirli dosyaları gerekebilir. Örneğin, bir .exe veya bir başlangıç betiği tooyour hizmet paketi tarafından kullanılan bir .msi dosyası tooadd isteyebilirsiniz. Veya tooadd bir web rolü ya da çalışan rolü projesi gerektiren bir derleme gerekiyor olabilir. eklenen Azure uygulamanız için toohello çözümü tooinclude dosyalar olması gerekir.

### <a name="tooinclude-files-in-hello-service-package"></a>Merhaba hizmet paketi tooinclude dosyaları
1. tooadd bir derleme tooa hizmet paketi hello aşağıdaki adımları kullanın:
   
   1. İçinde **Çözüm Gezgini** hello başvurulan derleme eksik hello projeniz için açık hello proje düğümü.
   2. tooadd hello derleme toohello projesi, açık hello kısayol menüsünü hello **başvuruları** klasörünü ve ardından **Başvuru Ekle**. Merhaba Başvuru Ekle iletişim kutusu görüntülenir.
   3. Tooadd istediğiniz ve hello seçin hello başvurusu seçin **Tamam** düğmesi.
      
      Merhaba başvuru hello altındaki toohello listesine eklenen **başvuruları** klasör.
   4. Eklediğiniz hello derleme hello kısayol menüsünü açın ve seçin **özellikleri**. Merhaba **özellikleri** penceresi görüntülenir.
      
      tooinclude bu derlemede hello hizmet paketini, hello **kopya yerel listesini** seçin **doğru**.
2. İçinde **Çözüm Gezgini** hello başvurulan derleme eksik hello projeniz için açık hello proje düğümü.
3. tooadd hello derleme toohello projesi, açık hello kısayol menüsünü hello **başvuruları** klasörünü ve ardından **Başvuru Ekle**. Merhaba **Başvuru Ekle** iletişim kutusu görüntülenir.
4. Tooadd istediğiniz ve hello seçin hello başvurusu seçin **Tamam** düğmesi.
   
    Merhaba başvuru hello altındaki toohello listesine eklenen **başvuruları** klasör.
5. Eklediğiniz hello derleme hello kısayol menüsünü açın ve seçin **özellikleri**. Merhaba Özellikler penceresi görünür.
6. tooinclude bu derlemede hello hizmet paketini, hello **kopya yerel** listesinde, seçin **doğru**.
7. tooinclude tooyour web rolü projesi, eklenen hello hizmet paketi dosyalarında hello dosya hello kısayol menüsünü açın ve ardından **özellikleri**. Merhaba gelen **özellikleri** penceresinde, seçin **içerik** hello gelen **yapı eylemi** liste kutusu.
8. tooinclude tooyour çalışan rolü projesi, eklenen hello hizmet paketi dosyalarında hello dosya hello kısayol menüsünü açın ve ardından **özellikleri**. Merhaba gelen **özellikleri** penceresinde, seçin **yeniyse Kopyala** hello gelen **kopyalama toooutput directory** liste kutusu.

## <a name="next-steps"></a>Sonraki adımlar
Visual Studio'da yayımlama tooAzure hakkında daha fazla toolearn bkz [Azure uygulaması Yayımlama Sihirbazı](vs-azure-tools-publish-azure-application-wizard.md).

