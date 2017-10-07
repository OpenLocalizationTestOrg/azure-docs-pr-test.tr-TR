---
title: "aaaEnabling eclipse'te Azure dağıtımları için uzaktan erişim"
description: "Nasıl tooenable uzaktan erişim için Eclipse hello Azure Araç Seti kullanarak Azure dağıtımları için öğrenin."
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
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Eclipse'te Azure dağıtımları için uzaktan erişimi etkinleştirme
toohelp dağıtımlarınızı sorun giderme, etkinleştirmek ve Uzaktan erişim tooconnect toohello sanal makine dağıtımınızı barındırma kullanmak. Uzak Masaüstü Protokolü (RDP) hello üzerinde Hello uzak erişim işlevini kullanır. TooAzure yayımladığınız veya bir Windows işletim sistemiyle Eclipse kullanıyorsanız, tooAzure yayımlamadan önce uzaktan erişim yapılandırabilirsiniz, uzaktan erişim dağıtımı için yapılandırabilirsiniz. Azure'da sipariş tooconnect tooyour dağıtımın sanal makine işletim sisteminizdeki ile uyumlu bir Uzak Masaüstü İstemcisi gerektiğine dikkat edin.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Önce uzaktan erişim tooenable tooAzure nasıl dağıtma
> [!NOTE]
> tooenable uygulama tooAzure dağıtmadan önce uzaktan erişim, Eclipse Windows üzerinde çalışan toobe gerekir.
> 
> 

Merhaba aşağıdaki resimde gösterilmiştir hello **uzaktan erişim** tooenable uzaktan erişim özellikleri iletişim kutusu kullanılır.

![][ic719494]

İki yolu toodisplay hello vardır **uzaktan erişim** Özellikleri iletişim kutusu:

* Merhaba tıklatın **Gelişmiş** hello bağlantıyı **uzaktan erişim** hello bölümünü **tooAzure yayımlama** iletişim.

* Açık hello **özellikleri** Azure projenizin iletişim.

Yeni bir Azure dağıtım projesi oluşturduğunuzda, hello proje uzak varsayılan olarak etkin erişemeyecektir. Ancak, kolayca uzaktan erişim hello hello kullanıcı adı ve parola belirterek etkinleştirebilirsiniz **tooAzure yayımlama** iletişim. Merhaba uzaktan erişim parolası X.509 sertifikaları kullanılarak şifrelenir. Kullanmıyorsanız, kendi sertifikanızı sağlamak hello şifreleme hello Eclipse için Azure eklentisi ile birlikte otomatik olarak imzalanan bir sertifika kullanır. Bu otomatik olarak imzalanan sertifika hello olan **cert** Azure projenizin klasörü hem bir ortak sertifika dosyası (SampleRemoteAccessPublic.cer) olarak depolanır ve bir kişisel bilgi değişimi (PFX) olarak sertifika dosyası ( SampleRemoteAccessPrivate.pfx). Merhaba ikinci hello hello sertifikanın özel anahtarı içerir ve bir varsayılan parolaya sahip **Parola1**. Bu parola ortak bilgi olduğundan, ancak hello varsayılan sertifika yalnızca Üretim dağıtımı için değil, amaçları için öğrenme için kullanılmalıdır. Tooenabled Uzak Oturumlar, dağıtımları için istediğiniz zaman bu nedenle dışındaki amacıyla öğrenme için hello tıklamanız **Gelişmiş** hello bağlantıyı **tooAzure yayımlama** iletişim toospecify kendi Sertifika. Bu Azure hello kullanıcı parolasının şifresini çözebilir şekilde tooupload hello PFX hello sertifika tooyour barındırılan hizmet hello Azure Yönetim Portalı içinde sürümü gerekeceğini unutmayın.

Merhaba kalan hello öğreticinin nasıl tooenable uzaktan erişim uzak erişim devre dışı başlangıçta oluşturulmuş bir Azure dağıtım projesi için gösterir. Bu öğreticinin amacı, yeni bir otomatik olarak imzalanan sertifika oluşturacağız ve kendi .pfx dosyasını tercih ettiğiniz bir parola gerekir. Bir sertifika yetkilisi tarafından verilen bir sertifikayı kullanarak hello seçeneğiniz de vardır.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Sonra uzaktan erişim tooenable tooAzure dağıtılan nasıl
tooAzure, aşağıdaki adımları kullanın hello dağıttıktan sonra tooenable uzaktan erişim:

1. Hello Azure yönetim portalında, Azure hesabınızı kullanarak oturum açın

2. Listenizde **bulut Hizmetleri**, dağıtılan bulut hizmetinizi seçin

3. Merhaba Hello bulut hizmeti web sayfasında, tıklatın **yapılandırma** bağlantı

4. Merhaba Hello alta hello yapılandırma sayfasında, tıklatın **uzak** bağlantı

5. Merhaba açılan iletişim kutusu görüntülendiğinde:
   
   * Merhaba rol belirtin, istediğiniz tooenable uzaktan erişim

   * Tooselect hello tıklatın **Uzak Masaüstü'nü etkinleştirme** onay kutusu
   
   * Bir kullanıcı adı ve Uzaktan erişim için toouse istediğiniz parolayı belirtin
   
   * Merhaba sertifika toouse seçin

6. **Tamam**’a tıklayın. 

Yapılandırma değişikliği birkaç dakika toocomplete sürebilir sürmekte olduğunu bildiren bir ileti görürsünüz. Hello yapılandırma değişikliği tamamlandıktan sonra hello hello adımları **toolog içinde uzaktan** bu makalenin sonraki bölümlerinde bölümü.

## <a name="how-tooenable-remote-access-in-your-package"></a>Tooenable uzaktan erişim nasıl paketinize
1. Eclipse'nın Proje Gezgini bölmesinde içinde Azure projenize sağ tıklatın ve **özellikleri**.

2. Merhaba, **özellikleri** iletişim kutusunda, genişletin **Azure** hello sol bölmedeki ve tıklatın **uzaktan erişim**.

3. Merhaba, **uzaktan erişim** iletişim kutusunda, olun **tüm rolleri tooaccept Uzak Masaüstü bağlantıları bu oturum açma kimlik bilgileri ile etkinleştirmek** denetlenir.

4. Merhaba Uzak Masaüstü bağlantısı için bir kullanıcı adı belirtin.

5. Belirtin ve hello hello kullanıcının parolasını onaylayın. Uzak Masaüstü Bağlantısı yaptığınızda bu iletişim kutusunda ayarladığınız hello kullanıcı adı ve parola değerlerini kullanılır. (Bu PFX parolanızı ayrı bir paroladan olduğunu unutmayın.)

6. Merhaba kullanıcı hesabı için Hello sona erme tarihi belirtin.

7. Tıklatın **yeni** toocreate yeni bir otomatik olarak imzalanan sertifika. (Alternatif olarak, çalışma alanı veya dosya sistemi hello aracılığıyla bir sertifika seçin **çalışma** veya **FileSystem** sırasıyla ancak biz oluşturacaksınız yeni bir Bu öğreticinin amaçları için düğmeler Sertifika.)

   * Merhaba, **yeni sertifika** iletişim kutusunda, belirtin ve onaylayın hello parola PFX dosyanız için kullanmanız.

   * İçin sağlanan hello değeri kabul **ad (CN)**, veya özel bir ad kullanın.

   * .Cer formunda, yeni sertifika hello kaydedileceği hello yolu ve dosya adını belirtin. Bu adım ve hello sonraki adım için hello kullanabilirsiniz **cert** Azure projeniz, ancak klasör boş toochoose olduğunuz başka bir konum. Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.cer**. (Merhaba oluşturma **c:\mycert** klasörü önceki tooproceeding ya da kullanmak isterseniz varolan bir klasöre.)

   * Merhaba yeni bir sertifika ve özel anahtarını, .pfx formunda kaydedileceği hello yolu ve dosya adını belirtin. Bu öğreticinin amaçları doğrultusunda kullanacağız **c:\mycert\mycert.pfx**. **Yeni sertifika** iletişim benzer toohello aşağıdaki görünmelidir (kullanmadıysanız, hello klasör yollarını Güncelleştir **c:\mycert**):
     
      ![][ic712275]

   * Tıklatın **Tamam** tooclose hello **yeni sertifika** iletişim.

8. **Uzaktan erişim** iletişim toohello aşağıdaki benzer görünmelidir:</p>
   
   ![][ic719495]

9. Tıklatın **Tamam** tooclose hello **uzaktan erişim** iletişim.

Uygulamanızı yeniden, hello ile dağıtım toocloud için kümesi oluşturun.

## <a name="toolog-in-remotely"></a>içinde toolog uzaktan
Rol örneği hazır olduktan sonra toohello sanal makineyi uygulamanızı barındıran uzaktan oturum açabilir.

* Windows ve, seçili hello Eclipse kullanıyorsanız **başlangıç Uzak Masaüstü'nü dağıtma** seçeneği dağıtımınızı başladığında, dağıtım tooAzure sırasında ile bir Uzak Masaüstü Bağlantısı oturum açma ekranı sunulur. Merhaba kullanıcı adı ve parola istendiğinde, hello uzak kullanıcı için belirtilen başlangıç değerleri girin ve de mümkün toolog olacaktır.

* İçinde başka bir şekilde toolog hello uzaktan olan <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Yönetim Portalı</a>:
  
  * Merhaba içinde **bulut Hizmetleri** hello Azure Yönetim Portalı görünümünü bulut hizmetiniz tıklatın, **örnekleri**, belirli bir örneğe tıklayın ve hello ardından **Bağlan**düğmesi. Merhaba **Bağlan** düğmesi görünür hello aşağıdaki hello komut çubuğunda olarak:
    
      ![][ic659273]

  * Başlangıç'ı tıklattıktan sonra **Bağlan** düğmesi, istendiğinde tooopen bir RDP dosyası olacaktır. Merhaba dosyasını açın ve hello istemleri izleyin. (Ayrıca bu dosya tooyour yerel bilgisayara kaydedin ve ardından hello dosyasını çift tıklatarak tooremote günlük tooyour içinde çalıştırmak toofirst gerek olmadan sanal makine hello yönetim portalına gidin.)

  * Merhaba kullanıcı adı ve parola istendiğinde, hello uzak kullanıcı için belirtilen başlangıç değerleri girin ve de mümkün toolog olacaktır.

> [!NOTE]
> Bir Windows olmayan işletim sisteminde varsa, toouse işletim sistemiyle uyumlu olan bir Uzak Masaüstü istemci gerekir ve istemci indirdiğiniz hello RDP dosyasındaki hello ayarları ile Merhaba adımları tooconfigure izleyin.
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse] 

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
