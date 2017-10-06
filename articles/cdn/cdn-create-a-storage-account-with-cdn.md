---
title: "bir Azure depolama hesabı Azure CDN ile aaaIntegrate | Microsoft Docs"
description: "Önbelleğe alma tarafından toouse hello Azure içerik teslim ağı (CDN) toodeliver yüksek bant genişliği içeriği Azure Storage'dan nasıl BLOB'öğrenin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Azure storage hesabı Azure CDN ile tümleştirme
CDN etkin toocache Azure depolama hesabınızdan içerik olabilir. Geliştiriciler BLOB'ları ve işlem örnekleri hello ABD, Avrupa, Asya, Avustralya ve Güney Amerika fiziksel düğümlerde, statik içeriği önbelleğe alarak yüksek bant genişliği içeriği teslimi için genel bir çözüm sunar.

## <a name="step-1-create-a-storage-account"></a>1. adım: depolama hesabı oluşturma
Aşağıdaki yordam toocreate bir Azure aboneliği için yeni bir depolama hesabı hello kullanın. Bir depolama hesabı için Azure storage hizmetlerine erişmenizi sağlar. Merhaba depolama hesabı hello ad'hello Azure depolama hizmeti bileşenlerinin her biri erişmek için en yüksek düzeyde hello temsil eder: Blob Hizmetleri, kuyruk Hizmetleri ve Tablo Hizmetleri. Daha fazla bilgi için toohello başvuran [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).

toocreate bir depolama hesabı, hello Hizmet Yöneticisi veya bir ortak yönetici için ilişkili hello olmalıdır abonelik.

> [!NOTE]
> Toocreate hello Azure Portal ve Powershell dahil olmak üzere bir depolama hesabı kullanabileceğiniz çeşitli yöntemler vardır.  Bu öğreticide, biz hello Azure Portal kullanacaksınız.  
> 
> 

**toocreate bir Azure aboneliği için bir depolama hesabı**

1. İçinde toohello oturum [Azure Portal](https://portal.azure.com).
2. Merhaba sol üst köşedeki, seçin **yeni**. Merhaba, **yeni** iletişim kutusunda **veri + depolama**, ardından **depolama hesabı**.
    
    Merhaba **depolama hesabı oluşturma** dikey penceresi görünür.   

    ![Depolama hesabı oluşturma][create-new-storage-account]  

3. Merhaba, **adı** alanında, bir alt etki alanı adı yazın. Bu giriş, 3-24 küçük harfler ve sayılar içerebilir.
   
    Bu değer hello hello hello aboneliği için Blob, kuyruk veya tablo kaynak adres için kullanılan URI içindeki konak adına dönüşür. Hello Blob hizmeti kapsayıcı kaynak adres için bir URI biçimi, aşağıdaki hello kullanırsınız nerede  *&lt;StorageAccountLabel&gt;*  yazmış toohello değeri başvuruyor **birURLgirin**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*
   
    **Önemli:** URL etiketi forms hello alt hello depolama hesabının URI hello ve azure'da barındırılan tüm hizmetler arasında benzersiz olması gerekir.
   
    Bu değer, ayrıca bu hesabı program aracılığıyla erişirken hello Portalı'nda veya bu depolama hesabını hello adı olarak kullanılır.
4. Merhaba Varsayılanları bırakabilir **dağıtım modeli**, **tür hesap**, **performans**, ve **çoğaltma**. 
5. Select hello **abonelik** hello depolama hesabı ile kullanılır.
6. Bir **Kaynak Grubu** seçin veya oluşturun.  Kaynak Grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Depolama hesabınız için bir konum seçin.
8. **Oluştur**'a tıklayın. Merhaba hello depolama hesabı oluşturma işlemi birkaç dakika toocomplete alabilir.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>2. adım: Hello depolama hesabı için CDN etkinleştirme

Merhaba yeni tümleştirmesi ile artık CDN depolama hesabınız için depolama portal uzantınızı ayrılmadan etkinleştirebilirsiniz. 

1. Merhaba depolama hesabını seçin, aşağı "CDN" ya da kaydırma hello sol gezinti menüsünde arayın, ardından "Azure CDN"'i tıklatın.
    
    Merhaba **Azure CDN** dikey penceresi görünür.

    ![CDN etkinleştir gezinme][cdn-enable-navigation]
    
2. Merhaba gerekli bilgileri girerek yeni bir uç noktası oluşturma
    - **CDN profili**: yeni oluşturun veya varolan bir profili kullanın.
    - **Fiyatlandırma katmanı**: yalnızca bir fiyatlandırma katmanı yeni bir CDN profili oluşturursanız, tooselect gerekir.
    - **CDN uç nokta adı**: tercih ettiğiniz her bir uç nokta adı girin.

    > [!TIP]
    > oluşturulan hello CDN uç noktası hello ana bilgisayar depolama hesabınızın adını varsayılan olarak kaynak kullanır.

    ! [cdn yeni uç nokta oluşturma] [cdn yeni-endpoint-oluşturma]

3. Oluşturulduktan sonra hello yeni uç nokta yukarıdaki hello uç nokta listesinde görünecektir.

    ![CDN depolama yeni uç noktası][cdn-storage-new-endpoint]

> [!NOTE]
> TooAzure CDN uzantısı tooenable CDN de gidebilirsiniz. [Öğreticisi](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>3. adım: ek CDN özellikleri etkinleştirme

Depolama hesabı "Azure CDN" dikey penceresinden hello listesi tooopen CDN yapılandırma dikey penceresinden hello CDN uç'a tıklayın. Sıkıştırma ve sorgu dizesi gibi teslimat için ek CDN özellikleri etkinleştirebilirsiniz coğrafi filtreleme. Ayrıca, özel etki alanı eşleme tooyour CDN uç noktası ekleyin ve özel etki alanı HTTPS etkinleştirin.
    
![CDN depolama cdn yapılandırması][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>4. adım: Erişim CDN içerik
tooaccess CDN Merhaba içeriğine önbelleğe alınmış, kullanım hello CDN URL'sine hello Portalı'nda sağlanan. önbelleğe alınan bir blob için başlangıç adresi benzer toohello şu olacaktır:

http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*BlobName*\>

> [!NOTE]
> CDN erişim tooa depolama hesabı için etkinleştirdiğinizde, genel olarak kullanılabilir tüm nesneler CDN uç önbelleğe alma için uygundur. Merhaba CDN şu anda önbelleğe alınmış nesneyi değiştirirseniz, önbelleğe alınmış hello içerik yaşam süresi süresi sona erdiğinde hello CDN içeriğini yeniler kadar hello yeni içerik CDN hello kullanılabilir olmayacaktır.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>5. adım: içerik CDN hello Kaldır
Artık toocache bir nesne hello Azure içerik teslim ağı (CDN) isterseniz, aşağıdaki adımları hello birini gerçekleştirebilirsiniz:

* Kapsayıcı özel ortak yerine hello yapabilirsiniz. Bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../storage/blobs/storage-manage-access-to-resources.md) daha fazla bilgi için.
* Devre dışı bırakmak veya hello CDN uç noktası hello yönetim portalını kullanarak silebilirsiniz.
* Barındırılan hizmet toono uzun yanıt toorequests hello nesnesi için değiştirebilirsiniz.

Zaten hello CDN önbelleğe alınmış nesneyi hello nesne için hello yaşam süresi süresi sona erene kadar veya hello endpoint temizlenir kadar önbelleğe alınmış olarak kalır. Merhaba yaşam süresi süresi sona erdiğinde, hello CDN hello CDN uç noktası hala geçerli olup olmadığını ve hello nesne hala anonim olarak erişilebilir toosee kontrol eder. Değilse, ardından hello nesne artık önbelleğe alınır.

## <a name="additional-resources"></a>Ek kaynaklar
* [Nasıl tooMap CDN içerik tooa özel etki alanı](cdn-map-content-to-custom-domain.md)
* [Özel etki alanınız için HTTPS'yi etkinleştir](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
