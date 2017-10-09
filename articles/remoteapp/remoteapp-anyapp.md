---
title: "aaaRun tüm Windows uygulamalarını Azure RemoteApp ile herhangi bir cihazda | Microsoft Docs"
description: "Bilgi nasıl tooshare tüm Windows uygulamalarını Azure RemoteApp kullanarak kullanıcılarınız."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Azure RemoteApp ile herhangi bir cihazda tüm Windows uygulamalarını çalıştırma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Yalnızca Azure RemoteApp kullanarak şu anda bir Windows uygulamasını gerçekten de her yerde her cihazda çalıştırabilirsiniz. İster 10 yıl önce yazılmış özel bir uygulamayı veya bir Office uygulaması olsun, kullanıcılarınız artık bağlı toobe tooa belirli işletim sistemine (Windows XP gibi) birkaç uygulama yok.

Azure RemoteApp ile kullanıcılarınız kendi Android de kullanabilirsiniz veya Apple cihazlarına ve get Windows (veya Windows Phone'daki) var aynı deneyimi hello. Bunun gerçekleştirilmesi Windows uygulamanızın Azure’daki bir Windows sanal makineler koleksiyonunda barındırılmasıyla sağlanır. Kullanıcılarınız, internete bağlanabildikleri her yerden bu makinelere erişebilir. 

Bir örneği için tam olarak nasıl okumaya toodo bu.

Bu makalede, tooshare erişim tüm kullanıcılarımızın yapacağız. Ancak, HERHANGİ bir uygulama kullanabilirsiniz. Uygulamanızı bir Windows Server 2012 R2 bilgisayara yükleyebilirsiniz sürece hello adımları kullanarak paylaşabilirsiniz. Merhaba gözden geçirebilirsiniz [uygulama gereksinimleri](remoteapp-appreqs.md) toomake emin uygulamanızı çalışır.

Lütfen bir veritabanı erişimi olduğundan ve bu veritabanı toobe yararlı istiyoruz olduğundan, biz fazladan birkaç adım toolet kullanıcılar istediğimizi Not hello Access veri paylaşımına erişin. Uygulamanız bir veritabanı değilse ya da, kullanıcıların toobe mümkün tooaccess bir dosya paylaşımı gerekmez, bu öğreticide adımları atlayabilirsiniz.

> [!NOTE]
> <a name="note"></a>Bu öğretici bir Azure hesabı toocomplete gerekir:
> 
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): krediler alırsınız tootry çıkışı Ücretli Azure hizmetlerini kullanabilirsiniz ve hatta kullanıldıktan sonra en fazla hello hesabı tutabilir ve ücretsiz Web siteleri gibi Azure hizmetlerini kullanabilirsiniz. Açıkça ayarlarınızı değiştirip ücret toobe isteyin sürece kredi kartınız asla ücretlendirilir.
> * [MSDN abone avantajlarını etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): MSDN aboneliğiniz, ücretli Azure hizmetlerinizi kullanabildiğiniz her ay size kredi verir.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>RemoteApp’te koleksiyon oluşturma
Önce bir koleksiyon oluşturun. Merhaba toplama, uygulama ve kullanıcılarınız için bir kapsayıcı görevi görür. Her koleksiyon bir görüntüyü temel alır. Kendi görüntünüzü oluşturabilir veya aboneliğinizle birlikte sağlanan bir görüntüyü kullanabilirsiniz. Bu öğretici için hello Office 2013 deneme görüntü kullanmakta olduğunuz - tooshare istiyoruz hello uygulama içerir.

1. Remoteapp'i görene kadar hello Azure portal, hello sol taraftaki gezinti ağacında ilerleyin. Bu sayfayı açın.
2. **Create a RemoteApp collection** (RemoteApp koleksiyonu oluştur) seçeneğine tıklayın.
3. **Hızlı oluştur**’a tıklayıp koleksiyonunuz için bir ad girin.
4. Toouse toocreate koleksiyonunuzu hello bölgesini seçin. Merhaba en iyi deneyim için coğrafi olarak en yakın olan hello bölgeyi seçin, kullanıcılarınızın hello uygulama erişim nerede toohello konumu. Örneğin, bu öğreticide, hello kullanıcılar Redmond, Washington konumundadır. Merhaba yakın Azure bölgesi **Batı ABD**.
5. Toouse hello fatura planı seçin. Merhaba standart fatura planında büyük bir Azure VM'de 10 kullanıcı sahipken hello temel fatura planı büyük bir Azure VM'ye 16 kullanıcı koyar. Genel bir örnek olarak, hello temel plan veri girişi türündeki iş akışlarında harika çalışır. Office gibi bir üretkenlik uygulaması hello standart Planı tercih etmelisiniz.
6. Son olarak, hello Office 2013 Professional görüntüsünü seçin. Bu görüntü Office 2013 uygulamalarını içerir. Söz konusu görüntünün yalnızca deneme koleksiyonları ve kavram kanıtları için uygun olduğunu anımsatmak isteriz. Bu görüntüyü bir üretim koleksiyonunda kullanamazsınız.
7. **Create RemoteApp collection** (RemoteApp koleksiyonunu oluştur) seçeneğine tıklayın.

![RemoteApp’te bulut koleksiyonu oluşturma](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Bu, koleksiyonunuzu oluşturma başlatır, ancak tooan saat sürebilir.

Şimdi, kullanıcılarınıza hazır tooadd demektir.

## <a name="share-hello-app-with-users"></a>Kullanıcılarla paylaşımını hello uygulama
Koleksiyonunuz başarıyla oluşturulduktan sonra zaman toopublish erişim toousers olduğu ve erişim tooit olmalıdır hello kullanıcılar ekleyin.

Merhaba koleksiyon oluşturulurken hello Azure RemoteApp düğümü çıktığınızda yaptıysanız hello Azure giriş sayfası ' tooit geri yolunuzu yaparak başlatın.

1. Ek seçenekler önceki tooaccess oluşturulan hello koleksiyona tıklayın ve hello koleksiyonu yapılandırın.
   ![Yeni bir RemoteApp bulut koleksiyonu](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. Merhaba üzerinde **yayımlama** sekmesini tıklatın, **Yayımla** Merhaba ekranında ve ardından hello altındaki **yayımlama Başlat menüsü programları**.
   ![RemoteApp programı yayımlama](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Merhaba listeden toopublish hello uygulamaları seçin. Bu konudaki hedefimiz için Access’i seçtik. **Tamamla**’ya tıklayın. Merhaba uygulamaları toofinish yayımlama için bekleyin.
   ![RemoteApp’te Access’i yayımlama](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Yayımlama Hello uygulama tamamladığında, toohello head **kullanıcı erişimini** tooadd tooyour uygulamaları erişmesi tüm hello kullanıcılar sekmesinde. Kullanıcılarınızın kullanıcı adlarını (e-posta adresi) girin ve **Kaydet**’e tıklayın.

![Kullanıcıların tooRemoteApp Ekle](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. Şimdi, zaman tootell geldi kullanıcılarınıza bu yeni uygulamalar hakkında ve nasıl tooaccess bunları. toodo Bu, kullanıcılarınızın bunları toohello Uzak Masaüstü İstemcisi indirme URL'si işaret eden bir e-posta gönderin.
   ![RemoteApp için Hello istemci indirme URL'si](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Erişim tooAccess yapılandırın
Bazı uygulamaların, RemoteApp aracılığıyla dağıtıldıktan sonra ek yapılandırmaya ihtiyaçları vardır. Özellikle, erişim için bir dosya paylaşımı tüm kullanıcıların erişebileceği Azure üzerinde devam eden toocreate çalışıyoruz. (Toodo istemiyorsanız oluşturabilirsiniz, bir [karma koleksiyon](remoteapp-create-hybrid-deployment.md) [bulut koleksiyonumuzun yerine] kullanıcılarınızın sağlayan erişim dosyaları ve bilgileri yerel ağınızdaki.) Ardından, biz bizim kullanıcılar toomap kendi bilgisayar toohello Azure dosya sistemi yerel bir sürücüde tootell gerekir.

hello Yöneticisi olarak bunu hello ilk bölümü. Sonra, kullanıcılarınızın gerçekleştireceği bazı adımlar vardır.

1. Yayımlama hello komut satırı arabirimi tarafından (cmd.exe) başlatın. Merhaba, **yayımlama** sekmesine **cmd**ve ardından **Yayımla > Publish program yolu kullanarak**.
2. Hello adını hello uygulama ve hello yolunu girin. Bu konudaki Hedefimiz için "Dosya Gezgini" Merhaba yolu olarak hello adı ve "% SYSTEMDRIVE%\windows\explorer.exe" olarak kullanın.
   ![Yayımlama Hello cmd.exe dosyası.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Toocreate Azure gereksinim artık [depolama hesabı](../storage/common/storage-create-storage-account.md). Biz hesabımıza "accessdepolama" adlı böylece anlamlı tooyou bir ad seçin. (toomisquote İskoçyalı, yalnızca bir "accessdepolama." olabilir) ![Azure depolama hesabımız](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Merhaba yolu tooyour depolama (uç nokta konumu) alabilmek için şimdi tooyour panoya geri dönün. Buna kısa bir süre sonra ihtiyacınız olacak, bu nedenle, bir yere kopyaladığınızdan emin olun.
   ![Merhaba depolama hesabı yolu](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. Ardından, Hello depolama hesabı oluşturulduktan sonra hello birincil erişim anahtarı gerekir. Tıklatın **erişim anahtarlarını Yönet**ve ardından kopyalama hello birincil erişim anahtarı.
6. Artık hello hello depolama hesabının bağlamını ayarlayın ve erişim için yeni bir dosya paylaşımı oluşturun. Cmdlet yükseltilmiş bir Windows PowerShell penceresinde aşağıdaki hello çalıştırın:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Bu nedenle paylaşımımız için çalıştıracağımız hello cmdlet'leri şunlardır:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

Şimdi, hello kullanıcının sırası kullanıcının. İlk olarak, kullanıcılarınızdan bir [RemoteApp istemcisi](remoteapp-clients.md) yüklemelerini isteyin. Ardından, hello kullanıcılar kendi hesabı toothat Azure dosya bir sürücüyü paylaşmak oluşturduğunuz toomap gerekir ve kendi Access dosyalarını ekleyin. Bunu aşağıdaki şekilde gerçekleştirirler.

1. Merhaba RemoteApp istemcisinde, yayımlanan uygulama erişim hello. Merhaba cmd.exe programını başlatın.
2. Komut toomap aşağıdaki hello bir sürücü bilgisayar toohello dosya paylaşımından çalıştırın:
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Merhaba ayarlarsanız **/ persistent** parametresi tooyes hello eşlenmiş sürücü kalıcı oturumlarında.
3. Şimdi, hello dosya Gezgini uygulamasını remoteapp'ten başlatın. Merhaba paylaşılan uygulama toohello dosya paylaşımında toouse istediğiniz tüm Access dosyalarını kopyalayın.
   ![Azure paylaşımına Access dosyası yerleştirme](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Son olarak, erişim açın ve sonra yeni paylaştığınız hello veritabanını açın. Verilerinizi hello buluttan çalıştırılan Access'te görmeniz gerekir.
   ![Merhaba buluttan çalıştırılan gerçek bir Access veritabanı](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

Artık bir RemoteApp istemcisi yüklemek şartıyla Access’i tüm cihazlarınızda kullanabilirsiniz.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
Artık koleksiyon oluşturmayı öğrendiğinize göre [Office 365 kullanan bir koleksiyon](remoteapp-tutorial-o365anywhere.md) oluşturmayı deneyin. İsterseniz, yerel ağınıza erişebilen bir [karma koleksiyon](remoteapp-create-hybrid-deployment.md) da oluşturabilirsiniz.

<!--Image references-->

