---
title: "Eclipse'te Azure dağıtımları için uzaktan erişimi etkinleştirme"
description: "Eclipse için Azure Araç Seti kullanarak Azure dağıtımları için uzaktan erişimi etkinleştirmek öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Eclipse'te Azure dağıtımları için uzaktan erişimi etkinleştirme
Dağıtımlarınızı gidermenize yardımcı olması için etkinleştirmek ve Uzaktan erişim, dağıtımınızı barındıran sanal makineye bağlanmak için kullanın. Uzak Masaüstü Protokolü (RDP) üzerinde uzak erişim işlevini kullanır. Azure'da yayımladınız veya bir Windows işletim sistemiyle Eclipse kullanıyorsanız, Azure'da yayımlamadan önce uzaktan erişim yapılandırabilirsiniz, uzaktan erişim dağıtımı için yapılandırabilirsiniz. Azure'daki dağıtımınızın sanal makineye bağlanmak için işletim sistemiyle uyumlu olan bir Uzak Masaüstü istemci gerektiğine dikkat edin.

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a>Azure'a dağıtmadan önce uzaktan erişim etkinleştirme
> [!NOTE]
> Uygulamanızı Azure'a dağıtmadan önce uzaktan erişimi etkinleştirmek için Eclipse Windows üzerinde çalışıyor olması gerekir.
> 
> 

Aşağıdaki resimde gösterildiği **uzaktan erişim** uzaktan erişimi etkinleştirmek için kullanılan özellikleri iletişim kutusu.

![][ic719494]

Görüntülenecek iki yolla **uzaktan erişim** Özellikleri iletişim kutusu:

* Tıklatın **Gelişmiş** bağlamak **uzaktan erişim** bölümünü **Azure Yayımla** iletişim.

* Açık **özellikleri** Azure projenizin iletişim.

Yeni bir Azure dağıtım projesi oluşturduğunuzda, projeyi uzak varsayılan olarak etkin erişemeyecektir. Ancak, kolayca uzaktan erişim kullanıcı adı ve parola belirterek etkinleştirebilirsiniz **Azure Yayımla** iletişim. Uzaktan erişim parolası X.509 sertifikaları kullanılarak şifrelenir. Kullanmıyorsanız, kendi sertifikanızı sağlamak Eclipse için Azure eklentisi ile birlikte otomatik olarak imzalanan bir sertifika şifreleme kullanır. Bu otomatik olarak imzalanan sertifika bulunduğu **cert** hem bir ortak sertifika dosyası (SampleRemoteAccessPublic.cer) ve bir kişisel bilgi değişimi (PFX) sertifika dosyası (SampleRemoteAccessPrivate.pfx) olarak depolanan projenizin Azure klasör. İkinci sertifikanın özel anahtarı içerir ve bir varsayılan parolaya sahip **Parola1**. Bu parola ortak bilgi olduğundan, ancak varsayılan sertifikayı amacıyla, Üretim dağıtımı için değil yalnızca öğrenme için kullanılmalıdır. Böylece dışındaki amacıyla öğrenme için etkin uzaktan oturumlar, dağıtımları için istediğinizde tıklamanız **Gelişmiş** bağlamak **Azure Yayımla** iletişim kutusunu kullanarak kendi sertifikanızı belirtin. Bu Azure kullanıcı parolasının şifresini çözebilir şekilde Azure Yönetim Portalı içinde barındırılan hizmetinize Sertifika PFX sürümünü yüklemek gerekeceğini unutmayın.

Öğretici geri kalanı ile uzaktan erişim devre dışı başlangıçta oluşturulmuş bir Azure dağıtım projesi için uzaktan erişimi etkinleştirmek nasıl gösterir. Bu öğreticinin amacı, yeni bir otomatik olarak imzalanan sertifika oluşturacağız ve kendi .pfx dosyasını tercih ettiğiniz bir parola gerekir. Ayrıca bir sertifika yetkilisi tarafından verilen bir sertifika kullanma seçeneğiniz vardır.

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a>Azure'a dağıttıktan sonra uzaktan erişim etkinleştirme
Azure'a dağıttıktan sonra uzaktan erişimi etkinleştirmek için aşağıdaki adımları kullanın:

1. Azure hesabınızı kullanarak Azure yönetim portalında oturum açın

2. Listenizde **bulut Hizmetleri**, dağıtılan bulut hizmetinizi seçin

3. Bulut hizmeti web sayfasını tıklatın **yapılandırma** bağlantı

4. Yapılandırma sayfasında altta tıklatın **uzak** bağlantı

5. Açılan iletişim kutusu görüntülendiğinde:
   
   * Uzaktan erişimi etkinleştirmek, için istediğiniz rolü belirtin

   * Seçmek için tıklatın **Uzak Masaüstü'nü etkinleştirme** onay kutusu
   
   * Bir kullanıcı adı ve Uzaktan erişim için kullanmak istediğiniz parolayı belirtin
   
   * Kullanılacak sertifikayı seçin

6. **Tamam**’a tıklayın. 

Yapılandırma değişikliği tamamlanması birkaç dakika sürebilir sürmekte olduğunu bildiren bir ileti görürsünüz. Yapılandırma değişikliği tamamlandıktan sonra adımları **uzaktan oturum açmak için** bu makalenin sonraki bölümlerinde bölümü.

## <a name="how-to-enable-remote-access-in-your-package"></a>Uzaktan erişim paketinize etkinleştirme
1. Eclipse'nın Proje Gezgini bölmesinde içinde Azure projenize sağ tıklatın ve **özellikleri**.

2. İçinde **özellikleri** iletişim kutusunda, genişletin **Azure** tıklatın ve sol bölmesinde **uzaktan erişim**.

3. İçinde **uzaktan erişim** iletişim kutusunda, olun **bu oturum açma kimlik bilgileri ile Uzak Masaüstü bağlantıları kabul etmek üzere tüm rolleri etkinleştir** denetlenir.

4. Uzak Masaüstü bağlantısı için bir kullanıcı adı belirtin.

5. Belirtin ve kullanıcının parolasını onaylayın. Uzak Masaüstü Bağlantısı yaptığınızda bu iletişim kutusunda ayarladığınız kullanıcı adı ve parola değerlerini kullanılır. (Bu PFX parolanızı ayrı bir paroladan olduğunu unutmayın.)

6. Kullanıcı hesabı için sona erme tarihi belirtin.

7. Tıklatın **yeni** yeni bir otomatik olarak imzalanan sertifika oluşturmak için. (Alternatif olarak, çalışma alanı veya dosya sistemi bir sertifika seçin **çalışma** veya **FileSystem** düğmeleri, sırasıyla ancak amacıyla Bu öğretici yeni bir sertifika oluşturacağız.)

   * İçinde **yeni sertifika** iletişim kutusunda, belirtin ve PFX dosyası için kullandığınız parolayı onaylayın.

   * İçin sağlanan değer kabul **ad (CN)**, veya özel bir ad kullanın.

   * .Cer formunda, yeni sertifikanın kaydedileceği yolu ve dosya adını belirtin. Bu adımı ve sonraki adım için kullanabileceğinizi **cert** klasörü Azure projeniz, ancak başka bir konum seçmek boş. Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.cer**. (Oluşturma **c:\mycert** devam etmeden veya kullanmak isterseniz var olan bir klasörü önce klasör.)

   * Yeni sertifikayı ve özel anahtarını, .pfx formunda kaydedileceği yolu ve dosya adını belirtin. Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.pfx**. **Yeni sertifika** iletişim aşağıdakine benzer görünmelidir (kullanmadıysanız, klasör yollarını güncelleştirme **c:\mycert**):
     
      ![][ic712275]

   * Tıklatın **Tamam** kapatmak için **yeni sertifika** iletişim.

8. **Uzaktan erişim** iletişim aşağıdakine benzer görünmelidir:</p>
   
   ![][ic719495]

9. Tıklatın **Tamam** kapatmak için **uzaktan erişim** iletişim.

Uygulamanızın, bulut dağıtımı için ayarlanmış yapı ile yeniden oluşturun.

## <a name="to-log-in-remotely"></a>Uzaktan oturum açmak için
Rol örneği hazır olduğunda, uzaktan uygulamanızı barındıran sanal makineye oturum açabilir.

* Windows ve seçtiğiniz Eclipse kullanıyorsanız **başlangıç Uzak Masaüstü'nü dağıtma** seçeneği dağıtımınızı başladığında Azure, dağıtım sırasında ile bir Uzak Masaüstü Bağlantısı oturum açma ekranı sunulur. Kullanıcı adı ve parola istendiğinde, uzak kullanıcı için belirtilen değerleri girin ve oturum açamaz.

* Uzaktan oturum açmak için başka bir yolunu <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Yönetim Portalı</a>:
  
  * İçinde **bulut Hizmetleri** görüntüleme Azure Yönetim Portalı'nın, bulut hizmeti,'ı tıklatın **örnekleri**, belirli bir örneğe tıklayın ve ardından **Bağlan** düğmesi. **Bağlan** düğmesi, komut çubuğunda aşağıdaki gibi görünür:
    
      ![][ic659273]

  * ' I tıklattıktan sonra **Bağlan** istenir bir RDP dosyasını açmak için düğmesi,. Dosyasını açın ve yönergeleri izleyin. (, De bu dosyayı yerel bilgisayarınıza kaydedin ve ardından, sanal makinenize uzaktan oturum açmak önce Yönetim Portalı'na gitmesini gerek kalmadan çift tıklayarak dosyayı çalıştırın.)

  * Kullanıcı adı ve parola istendiğinde, uzak kullanıcı için belirtilen değerleri girin ve oturum açamaz.

> [!NOTE]
> Bir Windows olmayan işletim sisteminde varsa, işletim sistemiyle uyumlu bir Uzak Masaüstü İstemcisi'ni kullanın ve indirdiğiniz RDP dosyasındaki ayarları ile istemci yapılandırma adımlarını izleyin gerekir.
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse] 

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
