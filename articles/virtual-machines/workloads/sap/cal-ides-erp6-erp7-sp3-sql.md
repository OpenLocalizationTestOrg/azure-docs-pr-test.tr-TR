---
title: "aaaDeploy SAP ERP 6.0 Azure üzerinde IDE EHP7 SP3 SAP | Microsoft Docs"
description: "Azure üzerinde SAP ERP 6.0 için SAP IDE EHP7 SP3 dağıtma"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a>Azure üzerinde SAP ERP 6.0 için SAP IDE EHP7 SP3 dağıtma
Bu makalede nasıl toodeploy bir SAP hello Windows işletim sistemi ve SQL Server ile SAP bulut Gereci kitaplığı (SAP CAL) 3.0 hello Azure üzerinde çalışan IDE sistem. Merhaba ekran görüntüleri hello işlem adım adım göstermektedir. farklı bir çözüme toodeploy izleyin hello aynı adımları.

Merhaba SAP CAL, Git toohello ile toostart [SAP bulut Gereci Kitaplığı](https://cal.sap.com/) Web sitesi. SAP de sahip bir blog hello hakkında yeni [SAP bulut Gereci kitaplığı 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience). 

> [!NOTE]
29 Mayıs 2017 hello Azure Resource Manager dağıtım modeli kullanabileceğiniz gibi ayrıca toohello daha az tercih edilen Klasik dağıtım modeli toodeploy hello SAP CAL. Merhaba yeni Resource Manager dağıtım modeli kullanır ve hello Klasik dağıtım modeli göz ardı öneririz.

Merhaba Klasik modeli kullanan bir SAP CAL hesabı zaten oluşturduysanız *başka bir SAP CAL hesabı toocreate gerek*. Bu hesap tooexclusively olmalıdır hello Resource Manager modelini kullanarak Azure'a dağıtabilirsiniz.

Toohello SAP CAL oturumu sonra hello ilk sayfa genellikle toohello sizi **çözümleri** sayfası. tooscroll bir bit, istediğiniz toofind hello çözüm gerekebilecek şekilde hello SAP CAL üzerinde sunulan hello çözümleri sürekli olarak artmaktadır. özel olarak Azure üzerinde kullanılabilir vurgulanmış hello SAP IDE Windows tabanlı çözüm hello dağıtım süreci gösterilmiştir:

![SAP CAL çözümleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a>Merhaba SAP CAL bir hesap oluşturun
1. hello için SAP CAL toohello toosign ilk kez SAP S kullanıcı veya SAP ile kayıtlı başka bir kullanıcı kullanın. Ardından azure'da hello SAP CAL toodeploy cihazları tarafından kullanılan bir SAP CAL hesap tanımlayın. Merhaba hesap tanımında şunları yapmanız gerekir:

    a. (Resource Manager veya Klasik) azure'da Hello dağıtım modelini seçin.

    b. Azure aboneliğiniz girin. Bir SAP CAL hesabı yalnızca tooone abonelik atanabilir. Birden fazla abonelik ihtiyacınız varsa, başka bir SAP CAL hesabı toocreate gerekir.
    
    c. Merhaba SAP CAL izni toodeploy Azure aboneliğinize verin.

    > [!NOTE]
    Merhaba sonraki adımlar nasıl toocreate bir SAP CAL hesap Resource Manager dağıtımları için gösterir. Bağlantılı toohello Klasik dağıtım modeli, SAP CAL hesabınız zaten varsa, *gerek* toofollow bu adımları toocreate yeni bir SAP CAL hesabı. Merhaba yeni SAP CAL hesabı hello Resource Manager modelinde toodeploy gerekir.

2. toocreate yeni bir SAP CAL hesabı, hello **hesapları** sayfa, Azure için iki seçenek gösterir: 

    a. **Microsoft Azure (Klasik)** hello Klasik dağıtım modeli ve artık tercih edilir.

    b. **Microsoft Azure** hello yeni Resource Manager dağıtım modeli.

    ![SAP CAL hesapları](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    Merhaba Resource Manager modelinde toodeploy seçin **Microsoft Azure**.

    ![SAP CAL hesapları](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. Hello Azure girin **abonelik kimliği** hello Azure portalı üzerinde bulunabilir. 

    ![SAP CAL abonelik kimliği](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. tanımladığınız tooauthorize hello SAP CAL toodeploy hello Azure aboneliği içine, tıklatın **Authorize**. Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:

    ![Oturum açma Internet Explorer bulut Hizmetleri](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. Birden fazla kullanıcı listeleniyorsa, hello Microsoft bağlantılı toobe hello Abonelikteki hello Seçtiğiniz Azure aboneliği olan bir hesap seçin. Sayfa aşağıdaki hello hello tarayıcı sekmesinde görünür:

    ![Internet Explorer bulut Hizmetleri onayı](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. Tıklatın **kabul**. Merhaba Yetkilendirme başarılı olursa yeniden hello SAP CAL hesabı tanımı görüntüler. Kısa bir süre sonra bir ileti hello yetkilendirme işleminin başarılı olduğunu onaylar.

7. Yeni oluşturulan SAP CAL hesabı tooyour kullanıcı tooassign Merhaba, girin, **kullanıcı kimliği** hello hello sağ taraftaki metin kutusu ve tıklatın **Ekle**. 

    ![Hesap toouser ilişkilendirme](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. Merhaba kullanıcı toohello SAP CAL toosign kullanmak hesabınızla tooassociate tıklatın **gözden**. 

9. Kullanıcı ve yeni oluşturulan hello SAP CAL hesabı arasında toocreate hello ilişkilendirme tıklayın **oluşturma**.

    ![Kullanıcı tooaccount ilişkilendirme](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

Olduğu bir SAP CAL hesabı başarıyla oluşturuldu:

- Merhaba Resource Manager dağıtım modeli kullanır.
- SAP sistemleri Azure aboneliğinize dağıtın.

> [!NOTE]
Windows ve SQL Server göre hello SAP IDE çözüm dağıtabilmeniz için önce bir SAP CAL abonelik kaydınızı toosign gerekebilir. Aksi takdirde hello çözümü olarak gösterebilir **kilitli** hello genel bakış sayfasında.

### <a name="deploy-a-solution"></a>Bir çözüm dağıtma
1. Bir SAP CAL hesabı kurduktan sonra seçin **SAP IDE çözüm Windows ve SQL Server üzerinde hello** çözümü. Tıklatın **örnek Oluştur**ve hello kullanım ve koşulları koşullar onaylayın. 

2. Merhaba üzerinde **temel mod: Örnek Oluştur** sayfasında gerekir:

    a. Bir örnek girmek **adı**.

    b. Bir Azure seçin **bölge**. Birden çok Azure bölgeleri sunulan bir SAP CAL abonelik tooget gerekebilir.

    c.  Hello Yöneticisi girin **parola** gösterildiği gibi hello çözüm:

    ![SAP CAL Basic modu: Örnek oluşturma](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. **Oluştur**'a tıklayın. Bir süre sonra hello boyutu ve karmaşıklığı (hello) SAP CAL tahmini sağlar, hello çözümün bağlı olarak hello durumu etkin ve kullanım için hazır olarak gösterilir: 

    ![SAP CAL örnekleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. toofind hello kaynak grubu ve tarafından oluşturulan tüm nesnelerini SAP CAL Merhaba, toohello Azure portalına gidin. Merhaba sanal makine aynı hello SAP CAL verilen adı örneği hello başlayarak bulunabilir.

    ![Kaynak grubu nesneleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. Dağıtılan toohello örnekleri Hello SAP CAL portalında gidin ve tıklayın **Bağlan**. açılır pencere aşağıdaki hello görünür: 

    ![Toohello örneğine bağlanma](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. Merhaba seçenekleri tooconnect dağıtılan toohello sistemlerinden birini kullanmadan önce tıklatın **Başlarken Kılavuzu**. Merhaba belgelerine adları kullanıcıların her hello bağlantı yöntemleri için hello. Merhaba parolaları olan kullanıcılar için tanımladığınız toohello ana parola hello hello dağıtım işleminin başında ayarlanır. Merhaba belgelerinde kullanabileceğiniz parolalarını ile daha işlevsel diğer kullanıcılar listelenir toohello toosign dağıtılan sistem.

    ![SAP Hoş Geldiniz belgeleri](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

Birkaç saat içinde sağlıklı bir SAP IDE sistem Azure'da dağıtılır.

Bir SAP CAL abonelik satın aldıysanız, SAP dağıtımlarınızı hello SAP CAL aracılığıyla Azure üzerinde tam olarak destekler. Merhaba destek BC VCM CAL sırasıdır.

