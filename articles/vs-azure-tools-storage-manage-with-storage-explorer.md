---
title: "aaaGet başlatılan Depolama Gezgini (Önizleme) | Microsoft Docs"
description: "Depolama Gezgini (Önizleme) ile Azure Storage kaynaklarını yönetme"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Depolama Gezgini (Önizleme) ile çalışmaya başlama
## <a name="overview"></a>Genel Bakış
Azure Depolama Gezgini (Önizleme), Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan tek başına bir uygulamadır. Bu makalede, hello Azure storage hesaplarınızı yönetmeye tooand bağlanma çeşitli yollarını öğrenin.

![Microsoft Azure Depolama Gezgini (Önizleme)][15]

## <a name="prerequisites"></a>Ön koşullar
* [Depolama Gezgini (Önizleme) indirip yükleme](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Tooa depolama hesabı veya hizmetine bağlanmak
Depolama Gezgini (Önizleme) tooconnect toostorage hesapları çeşitli yöntemler sağlar. Örneğin, şunları yapabilirsiniz:
* Azure aboneliği ile ilişkili toostorage hesaplarını bağlayın.
* Toostorage hesapları ve paylaşılan hizmetler diğer Azure aboneliklerinden bağlayın.
* Connect tooand hello Azure Storage öykünücüsü kullanarak yerel depolama yönetin. 

Ayrıca global ve ulusal Azure'daki depolama hesaplarıyla çalışabilirsiniz:

* [Tooan Azure aboneliğine bağlanma](#connect-to-an-azure-subscription): tooyour Azure aboneliğine ait depolama kaynaklarını yönetin.
* [İş yerel geliştirme depolama ile](#work-with-local-development-storage): hello Azure Storage öykünücüsü kullanarak yerel depolama yönetin.
* [Tooexternal depolama ekleme](#attach-or-detach-an-external-storage-account): tooanother Azure aboneliğine ait depolama kaynaklarını yönetmek veya hello depolama hesabının adını, anahtar ve uç noktaları kullanarak Azure Ulusal Bulutlar altında olan.
* [Bir SAS kullanarak bir depolama hesabı ekleme](#attach-storage-account-using-sas): paylaşılan erişim imzası (SAS) kullanılarak tooanother Azure aboneliğine ait depolama kaynaklarını yönetin.
* [Bir SAS kullanarak hizmet ekleme](#attach-service-using-sas): bir SAS kullanarak tooanother Azure aboneliğine ait belirli bir depolama hizmetini (blob kapsayıcısı, kuyruk veya tablo) yönetme.

## <a name="connect-tooan-azure-subscription"></a>Tooan Azure aboneliğine bağlanma
> [!NOTE]
> Bir Azure hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. Storage Explorer’da (Önizleme) **Azure Hesap ayarları**’nı seçin.

    ![Azure hesap ayarları][0]

2. Merhaba sol bölmede oturum açtığınız tüm hello Microsoft hesapları görüntülenir. tooconnect tooanother hesabı, select **Hesap Ekle**, en az bir etkin Azure aboneliği ile ilişkili bir Microsoft hesabıyla hello yönergeleri toosign izleyin.

    >[!NOTE]
    >Toonational Azure (örneğin, Azure Almanya, Azure kamu ve oturum açma aracılığıyla Azure Çin) bağlanması şu anda desteklenmiyor. Merhaba bkz "ekleme veya harici bir depolama hesabı ayırma" bölümü için nasıl tooconnect toonational Azure depolama hesapları.

3. Sonra başarıyla ile hello bölmesini doldurulmuş bir Microsoft hesabı, sol hello bu hesapla ilişkili Azure abonelikleri oturum açın. Select hello toowork ile istediğiniz ve ardından Azure abonelikleri **Uygula**. (Seçme **tüm abonelikleri** değiştirir veya hello hiçbirinin seçerek listelenen Azure aboneliklerinin.)

    ![Azure aboneliklerini seçme][3]  
    Hello sol bölmede seçili hello Azure abonelikleriyle ilişkilendirilen hello depolama hesapları gösterilir.

    ![Seçili Azure abonelikleri][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Tooan Azure yığın abonelik'e bağlanma

Bağlantı tooan Azure yığın aboneliği hakkında daha fazla bilgi için bkz: [bağlanmak Depolama Gezgini tooan Azure yığın abonelik](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Yerel geliştirme deposu ile çalışma
Depolama Gezgini (Önizleme) ile hello Azure Storage öykünücüsü kullanarak yerel depolama karşı çalışabilirsiniz. Bu yaklaşım hello depolama hesabı hello Azure Storage öykünücüsü tarafından öykündüğü için mutlaka Azure üzerinde dağıtılan bir depolama hesabı gerek kalmadan karşı kodu ve test depolama yazmanızı sağlar.

> [!NOTE]
> Hello Azure Storage öykünücüsü şu anda yalnızca Windows için desteklenmektedir.
>
>

1. Merhaba sol depolama Gezgini'nin (Önizleme) hello bölmesinde **(yerel ve iliştirildiği)** > **depolama hesapları** > **(Geliştirme)** düğümü.

    ![Yerel geliştirme düğümü][21]

2. Hello Azure Storage öykünücüsünü henüz yüklü değilse, istendiğinde toodo olan bir bilgi çubuğu aracılığıyla bunu. Merhaba bilgi çubuğu görüntülendiyse seçin **indirme hello en son sürümünü**ve ardından hello öykünücüsü yükleyin.

    ![Azure Storage Öykünücüsünü İndirme istemi][22]

3. Merhaba öykünücü yüklendikten sonra oluşturun ve yerel bloblar, kuyruklar ve tablolar ile çalışır. Her bir depolama hesabıyla toowork nasıl türü, toolearn hello aşağıdakilerden birini bakın:

    * [Azure blob depolama kaynaklarını yönetme](vs-azure-tools-storage-explorer-blobs.md)
    * Azure dosya paylaşımı depolama kaynaklarını yönetme: *Çok yakında*
    * Azure kuyruk depolama kaynaklarını yönetme: *Çok yakında*
    * Azure Tablo Depolama kaynaklarını yönetme - *Çok yakında*

## <a name="attach-or-detach-an-external-storage-account"></a>Harici bir depolama hesabı ekleme veya ayırma
Depolama Gezgini (Önizleme) ile depolama hesapları kolaylıkla paylaşılabilir böylece tooexternal depolama hesapları ekleyebilirsiniz. Bu bölümde nasıl tooattach too(and detach from) harici depolama hesapları.

### <a name="get-hello-storage-account-credentials"></a>Merhaba depolama hesabı bilgilerini al
tooshare harici bir depolama hesabı, hello hesabının sahibi söz konusu ilk hello hesabı için (hesap adı ve anahtar) hello kimlik bilgileri alın ve sonra bu bilgileri tooattach toothat (harici) hesabı isteyen hello kişiyle paylaşabilirsiniz gerekir. Merhaba aşağıdakileri yaparak hello depolama hesabının kimlik bilgilerini hello Azure portal aracılığıyla elde edebilirsiniz:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. **Gözat**’ı seçin.

3. **Depolama Hesapları**’nı seçin.

4. Merhaba üzerinde **depolama hesapları** dikey penceresinde, select hello istenen depolama hesabı.

5. Merhaba üzerinde **ayarları** hello dikey penceresinde seçili depolama hesabı, seçin **erişim anahtarları**.

    ![Erişim Anahtarları seçeneği][5]

6. Merhaba üzerinde **erişim anahtarları** dikey penceresinde, kopyalama hello **depolama hesabı adı** ve **key1** toohello depolama hesabı eklenirken kullanılacak değerler.

    ![Erişim tuşları][6]

### <a name="attach-tooan-external-storage-account"></a>Tooan harici depolama hesabı ekleme
tooattach tooan harici depolama hesabı, hello hesabın adı ve anahtarı gerekir. Bu değerleri tooobtain hello Azure portalına nasıl Hello "Get hello depolama hesabı kimlik" bölümde açıklanmaktadır. Ancak, hello Portalı'nda hello hesap anahtarı olarak adlandırılır **key1**. Hesap anahtarı için Depolama Gezgini (Önizleme) ister burada şekilde hello girin **key1** değeri.

1. Depolama Gezgini (Önizleme), seçin **tooAzure depolama birimini bağlayın**.

    ![TooAzure depolama seçeneği Bağlan][23]

2. Merhaba, **tooAzure depolama bağlanmak** iletişim kutusunda, hello hesap anahtarı belirtin (Merhaba **key1** hello Azure portal değerinden) ve ardından **sonraki**.

    > [!NOTE]
    > Ulusal Azure üzerinde bir depolama hesabından hello depolama bağlantı dizesi girebilirsiniz. Örneğin, tooconnect tooAzure Almanya depolama hesapları, bağlantı dizeleri benzer toohello aşağıdakileri girin: 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >Merhaba bağlantı dizesi hello Azure ' alabileceğiniz hello portal aynı şekilde açıklandığı gibi bölüm "Merhaba depolama hesabı bilgilerini al" Merhaba.

    ![Bağlan tooAzure depolama iletişim kutusu][24]

3. Merhaba, **harici depolama ekleme** iletişim kutusunda hello **hesap adı** kutusuna hello depolama hesabı adı girin, istediğiniz diğer ayarları belirtin ve ardından **sonraki**.

    ![Dış depolama ekle iletişim kutusu][8]

4. Merhaba, **bağlantı Özet** iletişim kutusunda, hello bilgilerini doğrulayın. Toochange herhangi bir şey istiyorsanız seçin **geri** ve istenen hello ayarlarını girin. 

5. **Bağlan**’ı seçin.

6. Başarıyla bağlandıktan sonra hello harici depolama hesabı ile görüntülenir **(harici)** toohello depolama hesabı adı eklenir.

    ![Sonuç tooan harici depolama hesabına bağlanma][9]

### <a name="detach-from-an-external-storage-account"></a>Harici bir depolama hesabı ayırma
1. Toodetach istediğiniz ve ardından hello harici depolama hesabına sağ **ayırma**.

    ![Depolama alanından ayırma seçeneği][10]

2. Merhaba onay iletisinde seçin **Evet** tooconfirm hello ayrılmayı hello harici depolama hesabından.

## <a name="attach-a-storage-account-by-using-an-sas"></a>SAS kullanarak depolama hesabı ekleme
Bir [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide Azure aboneliği kimlik gerek kalmadan geçici erişim tooa depolama hesabına vermek hello Yöneticisi bir Azure aboneliğinin olanak sağlar.

tooillustrate bu senaryo, şimdi bu Kullanıcıa bir Azure aboneliği Yöneticisi deyin olduğu ve Kullanıcıa istediği tooallow UserB tooaccess sınırlı bir süre çeşitli izinlerle bir depolama hesabı:

1. Kullanıcıa (Merhaba bağlantı dizesi hello depolama hesabı için oluşan) bir SAS dönemi ve istenen hello izinlerle belirli bir süre oluşturur.

2. Kullanıcıa paylaşımları SAS erişim toohello depolama hesabı isteyen hello kişiyle (örneğimizde, UserB) hello.  

3. Kullanıcıb kullanarak tooUserA ait Depolama Gezgini (Önizleme) tooattach toohello hesabı kullanan hello sağlanan SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Tooshare istediğiniz hello hesabı için bir SAS alma
1. Depolama Gezgini (Önizleme), paylaşımı ve ardından istediğiniz hello depolama hesabını sağ tıklatın **paylaşılan erişim imzası Al**.

    ![SAS alma içerik menüsü seçeneği][13]

2. Merhaba, **paylaşılan erişim imzası** iletişim kutusunda, hello zaman dilimi ve hello hesap için istediğiniz ve ardından izinleri belirtin **oluşturma**.

    ![SAS alma iletişim kutusu][14]  
    Merhaba **paylaşılan erişim imzası** iletişim kutusu açılır ve hello SAS görüntüler.

3. Sonraki toohello **bağlantı dizesi**seçin **kopya** toocopy, toohello Pano ve ardından **Kapat**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Merhaba SAS kullanarak paylaşılan toohello hesap ekleme
1. Depolama Gezgini (Önizleme), seçin **tooAzure depolama birimini bağlayın**.

    ![TooAzure depolama seçeneği Bağlan][23]

2. Merhaba, **tooAzure depolama bağlanmak** iletişim kutusu, hello bağlantı dizesini belirtin ve ardından **sonraki**.

    ![Bağlan tooAzure depolama iletişim kutusu][24]

3. Merhaba, **bağlantı Özet** iletişim kutusunda, hello bilgilerini doğrulayın. toomake değişiklikleri seçin **geri**ve ardından istediğiniz hello ayarlarını girin. 

4. **Bağlan**’ı seçin.

5. Bunu bağlandıktan sonra hello depolama hesabı ile görüntülenir **(SAS)** sağladığınız toohello hesap adı eklenir.

    ![SAS kullanarak hesap ekli tooan sonucu][17]

## <a name="attach-a-service-by-using-an-sas"></a>SAS kullanarak hizmet ekleme
Merhaba "bir SAS kullanarak bir depolama hesabı ekleme" bölümde, nasıl Azure abonelik yöneticisinin geçici erişim tooa depolama hesabı oluşturma ve hello depolama hesabı için bir SAS paylaşarak erişim izni verebilir açıklanmaktadır. Benzer şekilde bir depolama hesabının içinde belirli bir hizmet için (blob kapsayıcısı, kuyruk veya tablo) bir SAS oluşturulabilir.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Tooshare istediğiniz hello hizmeti için bir SAS oluşturmak
Bu bağlamda bir hizmet, bir blob kapsayıcısı, sıra veya tablo olabilir. toogenerate hello SAS listelenen hizmet için bkz:

* [Blob kapsayıcısı için Hello SAS alma](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Bir dosya paylaşımı için Hello SAS alma: *çok yakında*
* Bir kuyruk için SAS Hello alın: *çok yakında*
* Bir tablo için SAS Hello alın: *çok yakında*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>SAS kullanarak hizmet hello paylaşılan toohello hesap ekleme
1. Depolama Gezgini (Önizleme), seçin **tooAzure depolama birimini bağlayın**.

    ![TooAzure depolama seçeneği Bağlan][23]

2. Merhaba, **tooAzure depolama bağlanmak** iletişim kutusu, hello SAS URI'sini belirtin ve ardından **sonraki**.

    ![Bağlan tooAzure depolama iletişim kutusu][24]

3. Merhaba, **bağlantı Özet** iletişim kutusunda, hello bilgilerini doğrulayın. toomake değişiklikleri seçin **geri**ve ardından istediğiniz hello ayarlarını girin. 

4. **Bağlan**’ı seçin.

5. Bunu bağlandıktan sonra hello yeni eklenen hizmet hello altında görüntülenen **(hizmet SAS)** düğümü.

    ![Sonuç bir SAS kullanarak paylaşılan tooa hizmet ekleme][20]

## <a name="search-for-storage-accounts"></a>Depolama hesapları arama
Depolama hesaplarının uzun bir listeniz varsa, hızlı şekilde toolocate belirli bir depolama hesabını toouse hello arama hello sol bölmenin hello üstünde kutusudur.

Hello arama kutusuna yazarken hello bölmesini toothat noktası girmiş olduğunuz hello arama değeriyle eşleşen görüntüler hello depolama hesapları kalmadı. Örneğin, bir arama adı tüm depolama hesapları için içeren **tarcher** hello aşağıdaki ekran gösterilir:

![Depolama hesabı araması][11]

## <a name="next-steps"></a>Sonraki adımlar
* [Depolama Gezgini (Önizleme) ile Azure Blob Depolama kaynaklarını yönetme](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
