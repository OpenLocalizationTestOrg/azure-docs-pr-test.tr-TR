---
title: Azure Data Lake Store'da depolanan aaaSecuring verileri | Microsoft Docs
description: "Gruplar ve erişim kullanarak Azure Data Lake Store'da toosecure veri listeleri nasıl kontrol öğrenin"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Azure Data Lake Store içinde depolanan verilerin güvenliğini sağlama
Azure Data Lake Store'da verilerin güvenliğini sağlama üç adımlık bir yaklaşımdır.

1. Azure Active Directory (AAD içinde) güvenlik grupları oluşturarak başlayın. Bu güvenlik gruplarını kullanılan Azure Portalı'nda tooimplement rol tabanlı erişim denetimi (RBAC). Daha fazla bilgi için bkz: [Microsoft Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).
2. Merhaba AAD güvenlik gruplarının toohello Azure Data Lake Store hesabına atayın. Bu erişim toohello Data Lake Store hesabını hello portal ve yönetim işlemleri hello portalı veya API'ler denetler.
3. Merhaba Data Lake Store dosya sistemi üzerinde erişim denetimi listeleri (ACL'ler) gibi hello AAD güvenlik gruplarının atayın.
4. Ayrıca, Data Lake Store hello verilerine erişebilir istemciler için bir IP adresi aralığı ayarlayabilirsiniz.

Bu makalede yönergeler nasıl toouse hello Azure portal tooperform hello görevleri yukarıda sağlar. Data Lake Store hesabı ve veri hello düzeyinde güvenlik nasıl uyguladığını hakkında ayrıntılı bilgi için bkz: [Azure Data Lake Store'da güvenlik](data-lake-store-security-overview.md). ACL'ler Azure Data Lake Store içinde nasıl uygulandığını derin Dalış hakkında bilgi için bkz: [Data Lake Store'da erişim denetimine genel bakış](data-lake-store-access-control.md).

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Azure Active Directory'de güvenlik grupları oluşturma
Yönergeler için toocreate AAD güvenlik gruplarının ve nasıl tooadd kullanıcılar toohello Grup bkz [Azure Active Directory'de güvenlik gruplarını yönetme](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> Hello Azure portal kullanarak Azure AD'de, hem kullanıcılar hem de diğer grupları tooa grubu ekleyebilirsiniz. Bununla birlikte, içinde bir hizmet asıl tooa grubu tooadd sipariş, lütfen kullanın [Azure AD PowerShell Modülü](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Kullanıcıların veya güvenlik gruplarının tooAzure Data Lake Store hesaplarını atayın
Kullanıcıları atayın veya tooAzure Data Lake Store hesapları güvenlik gruplarını, erişim toohello yönetim işlemlerini hello Azure portalı ve Azure Resource Manager API'leri kullanılarak hello hesabındaki denetler. 

1. Bir Azure Data Lake Store hesabını açın. Hello sol bölmeden tıklatın **Gözat**, tıklatın **Data Lake Store**ve tooassign bir kullanıcı veya güvenlik grubu istediğiniz hello hesap adı toowhich hello Data Lake Store dikey penceresinden'ı tıklatın.

2. Data Lake Store hesabı ayarlar dikey penceresinde tıklayın **erişim denetimi (IAM)**. Varsayılan listeleri tarafından Hello dikey **abonelik yöneticileri** Grup sahibi olarak.
   
    ![Güvenlik grubu tooAzure Data Lake Store hesabını atamak](./media/data-lake-store-secure-data/adl.select.user.icon.png "Ata güvenlik grubu tooAzure Data Lake Store hesabı")

    Bir grup ve ata ilgili rollerin iki yolu tooadd vardır.
   
    * Bir kullanıcı/Grup toohello hesabı ekleyin ve ardından bir rol atayın veya
    * Bir rolü eklemek ve kullanıcıları/grupları toorole atayın.
     
    Bu bölümde, biz hello ilk yaklaşım, bir grup ekleme ve rol atama arayın. Benzer adımları toofirst seçin rol gerçekleştirmek ve grupları toothat rolü atayın.
4. Merhaba, **kullanıcılar** dikey penceresinde tıklatın **Ekle** tooopen hello **erişim Ekle** dikey. Merhaba, **erişim Ekle** dikey penceresinde tıklatın **bir rol seçin**ve ardından hello kullanıcı/grup için bir rol seçin.
   
    ![Merhaba kullanıcı için rol ekleme](./media/data-lake-store-secure-data/adl.add.user.1.png "hello kullanıcı için bir rol Ekle")
   
    Merhaba **sahibi** ve **katkıda bulunan** rol hello data lake hesabında erişim tooa çeşitli yönetim işlevleri sağlar. Merhaba veri gölü veri etkileşim kuracağı kullanıcılar için bunları toohello ekleyebilirsiniz ** okuyucu ** rol. Merhaba kapsamı bu rollerinin sınırlı toohello yönetim işlemlerini ilgili toohello Azure Data Lake Store hesabı değil.
   
    Verileri hello kullanıcıların ne işlemlerini tek tek dosya sistemi izinleri tanımlayın. Bu nedenle, okuyucu rolüne sahip bir kullanıcı hello hesabıyla ilişkilendirilmiş yalnızca görünüm yönetim ayarlarını yapabilirsiniz ancak büyük olasılıkla okuyabilir ve dosya sistemi izinleri toothem atanan verilerini alarak yazma. Data Lake Store dosya sistemi izinleri adresindeki açıklanmıştır [Ata güvenlik grubu ACL'ler toohello Azure Data Lake Store dosya sistemi olarak](#filepermissions).
5. Merhaba, **erişim Ekle** dikey penceresinde tıklatın **kullanıcıları eklemek** tooopen hello **kullanıcıları eklemek** dikey. Bu dikey penceresinde hello güvenlik grubu, Azure Active Directory'de daha önce oluşturduğunuz arayın. Grupları toosearch çok varsa, hello metin kutusu hello üst toofilter hello grup adı kullanın. **Seç**'e tıklayın.
   
    ![Güvenlik Grubu Ekle](./media/data-lake-store-secure-data/adl.add.user.2.png "güvenlik grubu Ekle")
   
    Listede olmayan bir grup/kullanıcı tooadd istiyorsanız, bunları hello kullanarak davet edebilirsiniz **davet** simgesi ve hello kullanıcı/Grup hello e-posta adresini belirtme.
6. **Tamam** düğmesine tıklayın. Merhaba güvenlik grubuna eklenen aşağıda gösterildiği gibi görmeniz gerekir.
   
    ![Güvenlik grubuna eklenen](./media/data-lake-store-secure-data/adl.add.user.3.png "güvenlik grubuna eklendi")

7. Kullanıcı/güvenlik grubunun artık erişim toohello Azure Data Lake Store hesabına sahiptir. Tooprovide erişim toospecific kullanıcıların istiyorsanız, bunları toohello güvenlik grubu ekleyebilirsiniz. Benzer şekilde, bir kullanıcı için toorevoke erişmek istiyorsanız, bunları hello güvenlik grubundan kaldırabilirsiniz. Ayrıca, birden çok güvenlik grupları tooan hesap atayabilirsiniz. 

## <a name="filepermissions"></a>Kullanıcı veya güvenlik grubu ACL'ler toohello Azure Data Lake Store dosya sistemi Ata
Toohello Azure Data Lake dosya sistemi kullanıcı/güvenlik gruplarına atayarak Azure Data Lake Store'da depolanan hello veriler üzerinde erişim denetimi ayarlayın.

1. Data Lake Store hesabı dikey pencerenizde, **Veri Gezgini**'ne tıklayın.
   
    ![Data Lake Store hesabında dizin oluşturmak](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Data Lake hesabında dizinler oluşturma")
2. Merhaba, **Veri Gezgini** dikey penceresinde hello dosya veya kendisi için tooconfigure hello ACL istediğiniz ve ardından klasörü tıklatın **erişim**. tooassign ACL tooa dosya tıklatmalıdır **erişim** hello gelen **Dosya Önizleme** dikey.
   
    ![Data Lake dosya sisteminde ACL'leri ayarlamak](./media/data-lake-store-secure-data/adl.acl.1.png "Data Lake dosya sistemi üzerindeki ACL'lerin ayarlayın")
3. Merhaba **erişim** dikey penceresinde hello standart erişim listelenir ve özel erişim toohello kök atanmış. Merhaba tıklatın **Ekle** simgesi tooadd Özel düzey ACL'ler.
   
    ![Liste standart ve özel erişim](./media/data-lake-store-secure-data/adl.acl.2.png "listesinde standart ve özel erişim")
   
   * **Standart erişim** hello sizin belirlediğiniz UNIX stili erişim, okuma, yazma, yürütme (rwx) toothree ayrı kullanıcı sınıfları: sahibi, Grup ve diğerleri.
   * **Özel erişim** tooset belirli adlandırılmış kullanıcıları veya grupları ve yalnızca hello dosyanın sahibi veya grup için izinler sağlar toohello POSIX ACL'ler karşılık gelir. 
     
     Daha fazla bilgi için bkz: [HDFS ACL'leri](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). ACL'ler Data Lake Store içinde nasıl uygulandığı hakkında daha fazla bilgi için bkz: [Data Lake Store'da erişim denetimi](data-lake-store-access-control.md).
4. Merhaba tıklatın **Ekle** simgesi tooopen hello **eklemek özel erişim** dikey. Bu dikey pencerede tıklatın **kullanıcı veya Grup Seç**ve ardından **kullanıcı veya Grup Seç** dikey penceresinde, Azure Active Directory'de daha önce oluşturduğunuz hello güvenlik grubu arayın. Grupları toosearch çok varsa, hello metin kutusu hello üst toofilter hello grup adı kullanın. Tooadd istediğiniz ve ardından hello grubu tıklatın **seçin**.
   
    ![Grup ekleme](./media/data-lake-store-secure-data/adl.acl.3.png "grup ekleme")
5. Tıklatın **Select izinleri**, hello izinler seçeneğini belirleyin ve varsayılan olarak ACL tooassign hello izinleri istediğinizi ACL ya da her ikisini de erişim. **Tamam** düğmesine tıklayın.
   
    ![İzinleri toogroup Ata](./media/data-lake-store-secure-data/adl.acl.4.png "izinleri toogroup atayın")
   
    Data Lake Store ve varsayılan/erişim ACL izinleri hakkında daha fazla bilgi için bkz: [Data Lake Store'da erişim denetimi](data-lake-store-access-control.md).
6. Merhaba, **eklemek özel erişim** dikey penceresinde tıklatın **Tamam**. Merhaba yeni eklenen grubuyla ilişkili hello izinleri şimdi hello listelenir **erişim** dikey.
   
    ![İzinleri toogroup Ata](./media/data-lake-store-secure-data/adl.acl.5.png "izinleri toogroup atayın")
   
   > [!IMPORTANT]
   > Merhaba geçerli sürümde, yalnızca 9 girişleri altında olabilir **özel erişim**. Birden fazla 9 kullanıcıların tooadd istiyorsanız, oluşturduğunuz güvenlik grupları, kullanıcıları toosecurity grupları eklemek için ekleme toothose güvenlik grupları hello Data Lake Store hesabı için erişim sağlar.
   > 
   > 
7. Merhaba Grup ekledikten sonra gerekirse hello erişim izinlerini değiştirebilirsiniz. Düz veya select hello onay kutusu her izin tooremove isteyip istemediğinizi dayalı (okuma, yazma, yürütme) yazın veya bu izni toohello güvenlik grubu atayın. Tıklatın **kaydetmek** toosave hello değişiklikleri veya **atmak** tooundo hello değişiklikleri.

## <a name="set-ip-address-range-for-data-access"></a>Veri erişimi için IP adres aralığını ayarlayın
Azure Data Lake Store, ağ düzeyinde erişim tooyour veri deposu toofurther kilitleme sağlar. Güvenlik duvarını etkinleştir, bir IP adresi belirtin veya güvenilen istemcileriniz için bir IP adresi aralığı tanımlayın. Bir kez etkinleştirildikten sonra hello IP adreslerini tanımlı aralığın içinde olan istemciler toohello deposu bağlanabilir.

![Güvenlik Duvarı ayarları ve IP erişim](./media/data-lake-store-secure-data/firewall-ip-access.png "Güvenlik Duvarı ayarları ve IP adresi")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Bir Azure Data Lake Store hesabı için güvenlik grupları kaldırın
Azure Data Lake Store hesaplarını güvenlik grupları kaldırdığınızda, hello Azure portalı ve Azure Resource Manager API'leri kullanılarak hello hesabındaki erişim toohello yönetim işlemlerini yalnızca değiştiriyorsunuz.

1. Data Lake Store hesabı dikey penceresinde tıklayın **ayarları**. Merhaba gelen **ayarları** dikey penceresinde tıklatın **kullanıcılar**.
   
    ![Güvenlik grubu tooAzure Data Lake hesabını atamak](./media/data-lake-store-secure-data/adl.select.user.icon.png "Ata güvenlik grubu tooAzure Data Lake hesabı")
2. Merhaba, **kullanıcılar** dikey tooremove istediğiniz hello güvenlik grubunu tıklayın.
   
    ![Güvenlik grubu tooremove](./media/data-lake-store-secure-data/adl.add.user.3.png "güvenlik grubu tooremove")
3. Merhaba güvenlik grubu için Hello dikey penceresinde tıklayın **kaldırmak**.
   
    ![Güvenlik grubu kaldırıldı](./media/data-lake-store-secure-data/adl.remove.group.png "güvenlik grubu kaldırıldı")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Güvenlik grubu ACL'ler Azure Data Lake Store dosya sisteminden kaldırın
Güvenlik grupları ACL'ler Azure Data Lake Store dosya sisteminden kaldırdığınızda, access toohello verilerini hello Data Lake Store değiştirin.

1. Data Lake Store hesabı dikey pencerenizde, **Veri Gezgini**'ne tıklayın.
   
    ![Data Lake hesabında dizin oluşturmak](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Data Lake hesabında dizinler oluşturma")
2. Merhaba, **Veri Gezgini** dikey penceresinde hello dosya veya tooremove hello ACL istediğiniz klasörü tıklatın ve, hesap dikey penceresinde hello ardından **erişim** simgesi. ACL tooremove bir dosya için tıklatmalıdır **erişim** hello gelen **Dosya Önizleme** dikey.
   
    ![Data Lake dosya sisteminde ACL'leri ayarlamak](./media/data-lake-store-secure-data/adl.acl.1.png "Data Lake dosya sistemi üzerindeki ACL'lerin ayarlayın")
3. Merhaba, **erişim** dikey penceresinde, hello **özel erişim** bölümünde, kullanmak istediğiniz tooremove hello güvenlik grubunu tıklatın. Merhaba, **özel erişim** dikey penceresinde tıklatın **kaldırmak** ve ardından **Tamam**.
   
    ![İzinleri toogroup Ata](./media/data-lake-store-secure-data/adl.remove.acl.png "izinleri toogroup atayın")

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
* [PowerShell kullanarak Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-powershell.md)
* [.NET SDK'yı kullanarak Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-net-sdk.md)
* [Data Lake Store'a ilişkin tanılama günlüklerine erişme](data-lake-store-diagnostic-logs.md)

