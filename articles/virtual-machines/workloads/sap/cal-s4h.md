---
title: SAP S/4HANA veya BW/4HANA Azure VM'de aaaDeploy | Microsoft Docs
description: "SAP S/4HANA veya BW/4HANA Azure VM'de dağıtın"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>SAP S/4HANA veya BW/4HANA azure'da dağıtmak
Bu makalede nasıl kullanarak toodeploy S/4HANA azure'da hello SAP bulut Gereci kitaplığı (SAP CAL) 3.0 açıklanmaktadır. toodeploy hello BW/4HANA gibi diğer SAP HANA tabanlı çözümleri uygulayın aynı adımları.

> [!NOTE]
Merhaba SAP CAL hakkında daha fazla bilgi için toohello Git [SAP bulut Gereci Kitaplığı](https://cal.sap.com/) Web sitesi. SAP de sahip bir blog hello hakkında [SAP bulut Gereci kitaplığı 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
29 Mayıs 2017 hello Azure Resource Manager dağıtım modeli kullanabileceğiniz gibi ayrıca toohello daha az tercih edilen Klasik dağıtım modeli toodeploy hello SAP CAL. Merhaba yeni Resource Manager dağıtım modeli kullanır ve hello Klasik dağıtım modeli göz ardı öneririz.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Adım adım işlemi toodeploy hello çözümü

Aşağıdaki ekran görüntüleri bir dizi hello nasıl kullanarak toodeploy S/4HANA azure'da hello SAP CAL gösterir. Merhaba işlemin çalıştığını hello BW/4HANA gibi diğer çözümleri için aynı şekilde.

Merhaba **çözümleri** sayfası gösterir hello bazıları SAP CAL HANA tabanlı çözümler kullanılabilir Azure üzerinde. **SAP S/4HANA 1610 FPS01, Fully-Activated Gereci** hello Orta sırada:

![SAP CAL çözümleri](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Merhaba SAP CAL bir hesap oluşturun
1. hello için SAP CAL toohello toosign ilk kez SAP S kullanıcı veya SAP ile kayıtlı başka bir kullanıcı kullanın. Ardından azure'da hello SAP CAL toodeploy cihazları tarafından kullanılan bir SAP CAL hesap tanımlayın. Merhaba hesap tanımında şunları yapmanız gerekir:

    a. (Resource Manager veya Klasik) azure'da Hello dağıtım modelini seçin.

    b. Azure aboneliğiniz girin. Bir SAP CAL hesabı yalnızca tooone abonelik atanabilir. Birden fazla abonelik ihtiyacınız varsa, başka bir SAP CAL hesabı toocreate gerekir.

    c. Merhaba SAP CAL izni toodeploy Azure aboneliğinize verin.

    > [!NOTE]
    Merhaba sonraki adımlar nasıl toocreate bir SAP CAL hesap Resource Manager dağıtımları için gösterir. Bağlantılı toohello Klasik dağıtım modeli, SAP CAL hesabınız zaten varsa, *gerek* toofollow bu adımları toocreate yeni bir SAP CAL hesabı. Merhaba yeni SAP CAL hesabı hello Resource Manager modelinde toodeploy gerekir.

2. Yeni bir SAP CAL hesabı oluşturun. Merhaba **hesapları** sayfa, Azure için üç seçeneğiniz gösterir: 

    a. **Microsoft Azure (Klasik)** hello Klasik dağıtım modeli ve artık tercih edilir.

    b. **Microsoft Azure** hello yeni Resource Manager dağıtım modeli.

    c. **Windows Azure 21Vianet tarafından işletilen** hello Klasik dağıtım modelini kullanan Çin'de bir seçenektir.

    Merhaba Resource Manager modelinde toodeploy seçin **Microsoft Azure**.

    ![SAP CAL hesap ayrıntıları](./media/cal-s4h/s4h-pic-2a.png)

3. Hello Azure girin **abonelik kimliği** hello Azure portalı üzerinde bulunabilir.

   ![SAP CAL hesapları](./media/cal-s4h/s4h-pic3c.png)

4. tanımladığınız tooauthorize hello SAP CAL toodeploy hello Azure aboneliği içine, tıklatın **Authorize**. Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:

   ![Oturum açma Internet Explorer bulut Hizmetleri](./media/cal-s4h/s4h-pic4c.png)

5. Birden fazla kullanıcı listeleniyorsa, hello Microsoft bağlantılı toobe hello Abonelikteki hello Seçtiğiniz Azure aboneliği olan bir hesap seçin. Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:

   ![Internet Explorer bulut Hizmetleri onayı](./media/cal-s4h/s4h-pic5a.png)

6. Tıklatın **kabul**. Merhaba Yetkilendirme başarılı olursa yeniden hello SAP CAL hesabı tanımı görüntüler. Kısa bir süre sonra bir ileti hello yetkilendirme işleminin başarılı olduğunu onaylar.

7. Yeni oluşturulan SAP CAL hesabı tooyour kullanıcı tooassign Merhaba, girin, **kullanıcı kimliği** hello hello sağ taraftaki metin kutusu ve tıklatın **Ekle**.

   ![Hesap toouser ilişkilendirme](./media/cal-s4h/s4h-pic8a.png)

8. Merhaba kullanıcı toohello SAP CAL toosign kullanmak hesabınızla tooassociate tıklatın **gözden**. 
 
9. Kullanıcı ve yeni oluşturulan hello SAP CAL hesabı arasında toocreate hello ilişkilendirme tıklayın **oluşturma**.

   ![Kullanıcı tooSAP CAL hesabı ilişkisi](./media/cal-s4h/s4h-pic9b.png)

Olduğu bir SAP CAL hesabı başarıyla oluşturuldu:

- Merhaba Resource Manager dağıtım modeli kullanır.
- SAP sistemleri Azure aboneliğinize dağıtın.

Şimdi kullanıcı aboneliğinizde Azure içine toodeploy S/4HANA başlatabilirsiniz.

> [!NOTE]
Devam etmeden önce Azure H-serisi VM'ler için Azure çekirdek kotaları yüklü olup olmadığını belirler. Merhaba şu anda, H-serisi VM'ler Azure toodeploy hello SAP CAL kullanan bazı hello SAP HANA tabanlı çözümler. Azure aboneliğiniz H-seri için hiçbir H-serisi çekirdek kota sahip olmayabilir. Bu durumda, toocontact Azure destek tooget en az 16 H-serisi çekirdek kotası gerekebilir.

> [!NOTE]
Bir çözümde azure'da hello SAP CAL dağıttığınızda, yalnızca bir Azure bölgesi seçebilirsiniz bulabilirsiniz. toodeploy Azure bölgeleri hello dışında bir SAP CAL hello tarafından önerilen, toopurchase SAP CAL abonelikten gerekir. Azure bölgeleri hello Başlangıçta önerilen olanlar dışındaki CAL hesap etkinleştirildi toodeliver tooopen SAP toohave içeren bir ileti da gerekebilir.

### <a name="deploy-a-solution"></a>Bir çözüm dağıtma

Şimdi hello bir çözüm dağıtma **çözümleri** hello SAP CAL sayfası. Merhaba SAP CAL iki sıraları toodeploy sahiptir:

- Dağıtılan bir sayfa toodefine hello sistem toobe kullanan bir temel sıralı
- Gelişmiş dizisi VM boyutlarını belirli seçenekler sunar 

Biz hello temel yolu buraya toodeployment göstermektedir.

1. Merhaba üzerinde **hesap ayrıntıları** sayfasında gerekir:

    a. SAP CAL hesabı seçin. (Merhaba Resource Manager dağıtım modeli ile ilişkili toodeploy olan bir hesap kullanın.)

    b. Bir örnek girmek **adı**.

    c. Bir Azure seçin **bölge**. Merhaba SAP CAL bir bölge önerir. Başka bir Azure bölgesi gerekir ve bir SAP CAL aboneliğiniz yoksa, SAP tooorder bir CAL abonelikle gerekir.

    d. Asıl girin **parola** hello çözüm sekiz veya dokuz karakter. Merhaba parola hello farklı bileşenleri hello Yöneticiler için kullanılır.

   ![SAP CAL Basic modu: Örnek oluşturma](./media/cal-s4h/s4h-pic10a.png)

2. Tıklatın **oluşturma**, görüntülenen hello ileti kutusunda tıklatıp **Tamam**.

   ![SAP CAL VM boyutları desteklenir](./media/cal-s4h/s4h-pic10b.png)

3. Merhaba, **özel anahtar** iletişim kutusu, tıklatın **deposu** toostore hello özel anahtar hello SAP CAL. Merhaba özel anahtar için toouse parola koruması **karşıdan**. 

   ![SAP CAL özel anahtar](./media/cal-s4h/s4h-pic10c.png)

4. Okuma hello SAP CAL **uyarı** tıklayın ve ileti **Tamam**.

   ![SAP CAL uyarı](./media/cal-s4h/s4h-pic10d.png)

    Şimdi hello dağıtım gerçekleşir. Bir süre sonra hello boyutu ve karmaşıklığı (hello) SAP CAL tahmini sağlar, hello çözümün bağlı olarak hello durumu etkin ve kullanım için hazır olarak gösterilir.

5. toofind hello sanal makineler ile toplanan diğer ilişkili kaynakları bir kaynak grubunda Merhaba, toohello Azure portalına gidin: 

   ![Dağıtılan Hello yeni portalında SAP CAL nesneler](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. Merhaba SAP CAL portalında olarak hello durumu görünür **etkin**. tooconnect toohello çözüm tıklatın **Bağlan**. Farklı seçenekler tooconnect toohello farklı bileşenleri bu çözüm içinde dağıtılır.

   ![SAP CAL örnekleri](./media/cal-s4h/active_solution.png)

7. Merhaba seçenekleri tooconnect dağıtılan toohello sistemlerinden birini kullanmadan önce tıklatın **Başlarken Kılavuzu**. 

   ![Toohello örneğine bağlanma](./media/cal-s4h/connect_to_solution.png)

    Merhaba belgelerine adları kullanıcıların her hello bağlantı yöntemleri için hello. Merhaba parolaları olan kullanıcılar için tanımladığınız toohello ana parola hello hello dağıtım işleminin başında ayarlanır. Merhaba belgelerinde kullanabileceğiniz parolalarını ile daha işlevsel diğer kullanıcılar listelenir toohello toosign dağıtılan sistem. 

    Merhaba Windows Uzak Masaüstü makinede hello önceden yüklenmiş olarak SAP GUI kullanırsanız, örneğin, hello S/4 sistem şuna benzeyebilir:

   ![Merhaba SM50 SAP GUI önceden yüklenmiş](./media/cal-s4h/gui_sm50.png)

    Veya hello DBACockpit kullanırsanız, hello örnek şuna benzeyebilir:

   ![Merhaba DBACockpit SAP GUI SM50](./media/cal-s4h/dbacockpit.png)

Birkaç saat içinde sağlıklı bir SAP S/4 Gereci Azure'da dağıtılır.

Bir SAP CAL abonelik satın aldıysanız, SAP dağıtımlarınızı hello SAP CAL aracılığıyla Azure üzerinde tam olarak destekler. Merhaba destek BC VCM CAL sırasıdır.







