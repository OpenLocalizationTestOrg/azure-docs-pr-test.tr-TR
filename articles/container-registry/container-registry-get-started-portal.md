---
title: "aaaCreate özel Docker kayıt defteri - Azure portalı | Microsoft Docs"
description: "Oluşturma ve yönetme özel Docker kapsayıcısı kayıt defterleri hello Azure portal ile çalışmaya başlama"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Hello Azure portal kullanarak özel bir Docker kapsayıcısı kayıt oluşturun
Hello Azure portal toocreate bir kapsayıcı kayıt defteri kullanın ve ayarlarını yönetin. Ayrıca oluşturmak ve kapsayıcı kayıt defterleri hello kullanarak yönetmek [Azure CLI 2.0 komutları](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) veya program aracılığıyla hello kapsayıcı kayıt defteri [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).

Arka plan ve kavramları için bkz: [genel bakış hello](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Kapsayıcı kayıt defteri oluşturma
1. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **+ yeni**.
2. Arama hello Market **Azure kapsayıcı kayıt defteri**.
3. Yayımcısı **Microsoft** olan **Azure Kapsayıcı Kayıt Defteri** uygulamasını seçin.
    ![Azure Market’te Container Kayıt Defteri hizmeti](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. **Oluştur**'a tıklayın. Merhaba **Azure kapsayıcı kayıt defteri** dikey penceresi görünür.

    ![Container kayıt defteri ayarları](./media/container-registry-get-started-portal/container-registry-settings.png)
5. Merhaba, **Azure kapsayıcı kayıt defteri** dikey penceresinde, aşağıdaki bilgilerle hello girin. İşiniz bittiğinde **Oluştur**’a tıklayın.

    a. **Kayıt defteri adı**: Oluşturduğunuz kayıt defterinize özel olan, genel olarak benzersiz bir üst düzey etki alanı adı. Bu örnekte hello kayıt defteri adıdır *myRegistry01*, ancak kendi benzersiz adı değiştirin. Merhaba ad yalnızca harfler ve sayılar içerebilir.

    b. **Kaynak grubu**: Varolan seçin [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) veya yeni bir hello adını yazın.

    c. **Konum**: hello hizmet olduğu bir Azure veri merkezi konum seçin [kullanılabilir](https://azure.microsoft.com/regions/services/), gibi **Orta Güney ABD**.

    d. **Yönetici kullanıcı**: istiyorsanız, bir yönetici kullanıcı tooaccess hello kayıt defteri etkinleştirin. Merhaba kayıt defteri oluşturduktan sonra bu ayarı değiştirebilirsiniz.

      > [!IMPORTANT]
      > Ayrıca bir yönetici kullanıcı hesabıyla erişim tooproviding, kapsayıcı kayıt defterleri Azure Active Directory hizmet asıl adı tarafından desteklenen kimlik doğrulama desteği. Daha fazla bilgi ve göz önünde bulundurulması gereken diğer noktalar için bkz. [Kapsayıcı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).
      >

    e. **Depolama hesabı**: hello varsayılan ayarı toocreate kullanmak bir [depolama hesabı](../storage/common/storage-introduction.md), veya mevcut bir depolama hesabını hello seçin aynı konumu. Premium Depolama şu anda desteklenmemektedir.

## <a name="manage-registry-settings"></a>Kayıt defteri ayarlarını yönetme
Merhaba kayıt defteri oluşturduktan sonra hello kayıt defteri ayarları hello başlatarak **kapsayıcı kayıt defterleri** dikey penceresinde hello portal. Örneğin, hello ayarları toolog tooyour kayıt defterinde gerekebilir veya tooenable istediğiniz veya hello yönetici kullanıcıyı devre dışı olabilir.

1. Merhaba üzerinde **kapsayıcı kayıt defterleri** dikey penceresinde, kayıt defteri hello adına tıklayın.

    ![Container kayıt defteri dikey penceresi](./media/container-registry-get-started-portal/container-registry-blade.png)
2. toomanage erişim ayarlar'ı **erişim tuşu**.

    ![Container kayıt defteri erişimi](./media/container-registry-get-started-portal/container-registry-access.png)
3. Ayarları aşağıdaki hello dikkat edin:

   * **Oturum açma sunucusu** -hello tam adı toohello kayıt defterinde toolog kullanın. Bu örnekte bu değer `myregistry01.azurecr.io`’dur.
   * **Yönetici kullanıcı** - geçiş tooenable veya hello kayıt defterindeki yönetici kullanıcı hesabı devre dışı bırakın.
   * **Kullanıcı adı** ve **parola** -(etkinse) hello yönetici kullanıcı hesabının kimlik bilgilerini hello toohello kayıt defterinde toolog kullanabilirsiniz. İsteğe bağlı olarak hello parolaları yeniden oluşturabilirsiniz. İki parola bağlantıları toohello kayıt defteri hello yeniden oluşturmak, bir parola kullanarak diğer parola bulundurabilirsiniz şekilde oluşturulur. Bunun yerine, bir hizmet asıl tooauthenticate bkz [özel Docker kapsayıcısı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme](container-registry-get-started-docker-cli.md)
