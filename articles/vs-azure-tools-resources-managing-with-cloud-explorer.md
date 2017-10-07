---
title: aaaManaging Azure Cloud Explorer kaynaklarla | Microsoft Docs
description: "Bilgi nasıl toouse Cloud Explorer toobrowse ve Visual Studio içinde Azure kaynaklarını yönetin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Visual Studio Cloud Explorer'da, Azure hesaplarıyla ilişkili hello kaynaklarını yönetme
Cloud Explorer, tooview Azure kaynaklarınızı etkinleştirir ve kaynak grupları, bunların özelliklerini inceleyebilir ve Visual Studio içinde anahtar Geliştirici tanılama eylemleri gerçekleştirin. 

Hello gibi [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer hello Azure Kaynak Yöneticisi yığınında oluşturulur. Bu nedenle, Cloud Explorer anlar Azure kaynak gruplarını gibi kaynakları ve Logic apps ve API uygulamaları gibi Azure Hizmetleri ve destekliyorsa [rol tabanlı erişim denetimi](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Ön koşullar
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) hello ile **Azure iş yükü** seçili veya önceki bir sürümünü Visual Studio ile Merhaba [.NET 2.9 için Microsoft Azure SDK'sı](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Microsoft Azure hesabı - bir hesabınız yoksa, şunları yapabilirsiniz [ücretsiz deneme için kaydolun](http://go.microsoft.com/fwlink/?LinkId=623901) veya [Visual Studio abone Avantajlarınızı etkinleştirebilir](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> tooview Cloud Explorer seçin **Görünüm** > **Cloud Explorer** hello menü çubuğunda.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Bir Azure hesabı tooCloud Explorer ekleme
bir Azure hesabı ile ilişkili tooview hello kaynakları hello hesap tooCloud Explorer ilk eklemeniz gerekir. 

1. İçinde **Cloud Explorer**seçin **Azure hesap ayarlarını**.

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Seçin **yeni hesap eklemek**. 

    ![Cloud Explorer hesabı Ekle bağlantı](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Toohello kaynakları istediğiniz Azure hesabı oturum toobrowse. 

1. Tooan Azure hesabı oturum sonra bu hesapla ilişkili hello abonelikleri görüntüler. Merhaba toobrowse istediğiniz ve ardından hello hesap aboneliklerinin onay kutularını seçin **Uygula**. 
 
    ![Cloud Explorer: Azure abonelikleri toodisplay seçin](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Kaynakları istediğiniz hello abonelikleri seçtikten sonra toobrowse, bu abonelikleri ve kaynakları hello Cloud Explorer görüntüler.

    ![Cloud Explorer kaynak bir Azure hesabı için listeleme](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Bir Azure hesabı bulut gezgininden Kaldır 

1. İçinde **Cloud Explorer**seçin **Azure hesap ayarlarını**.

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Sonraki toohello hesabı tooremove, istediğiniz **kaldırmak**.

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Kaynak türleri veya kaynak gruplarını görüntüleme
tooview ya da seçin, Azure kaynaklarınıza **kaynak türleri** veya **kaynak grupları** görünümü.

1. İçinde **Cloud Explorer**, select hello kaynak görünümü açılır.

    ![Cloud Explorer açılır liste tooselect istenen hello kaynakları görünümü](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. Merhaba bağlam menüsünden istenen hello görünümü seçin: 

    - **Kaynak türleri** görünümü - hello üzerinde kullanılan hello ortak [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), web uygulamaları, depolama hesapları ve sanal makineler gibi kendi türüne göre kategorize Azure kaynaklarınızı gösterir. 
    - **Kaynak grupları** view - kategorilere ayıran Azure kaynakları ile bunların ilişkili hello Azure kaynak grubu tarafından. Bir kaynak grubu genellikle belirli bir uygulama tarafından kullanılan Azure kaynaklarını paketidir. Azure kaynak grupları hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış](./azure-resource-manager/resource-group-overview.md).

    Merhaba aşağıdaki resimde hello karşılaştırması iki kaynak görünümleri gösterilmektedir:

    ![Cloud Explorer kaynak görünümleri karşılaştırma](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Görüntülemek ve bulut Explorer'da kaynaklara gidin
Azure kaynak toonavigate tooan ve Cloud Explorer'da bilgilerini görüntülemek, hello öğenin türü veya ilişkili kaynak grubunu genişletin ve ardından hello kaynak seçin. Bir kaynak seçtiğinizde, bilgi hello iki sekmeleri - görünür **Eylemler** ve **özellikleri** - Cloud Explorer hello sonundaki. 

- **Eylemler** sekmesi - listeleri hello eylemler için seçili hello kaynak Cloud Explorer'da alabilir. Ayrıca bu seçenekler hello kaynak tooview sağ tıklayarak bağlam menüsünü görüntüleyebilirsiniz.

- **Özellikler** sekmesi - olduğu ilişkili türü, yerel ayar ve kaynak grubu gibi hello kaynak hello özelliklerini gösterir.

Merhaba aşağıdaki resimde, her bir sekmede bir uygulama hizmeti için gördüğünüz bir örnek karşılaştırması gösterilmektedir:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Her kaynak hello eyleminin **portalında açık**. Bu eylem seçtiğinizde, bulut Explorer seçili hello kaynak hello görüntüler. [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040). Merhaba **portalında açık** özelliktir iç içe geçmiş toodeeply kaynakları gezinmek için kullanışlı.

Ek eylemleri ve özellik değerlerini de hello Azure kaynak üzerinde tabanlı görünebilir. Örneğin, web uygulamaları ve logic apps hello eylemleri de **tarayıcıda aç** ve **hata ayıklayıcısını** ayrıca çok**portalında açık**. Depolama hesabı blob, kuyruk veya tablo seçtiğinizde Eylemler tooopen düzenleyicileri görünür. Azure uygulamaları **URL** ve **durum** depolama kaynaklarını anahtar ve bağlantı dizesi özellikleri varken özellikleri.

## <a name="find-resources-in-cloud-explorer"></a>Cloud Explorer'da kaynakları bulun
Azure hesabı aboneliklerinizi belirli bir adla toolocate kaynaklarla hello hello adı girin **arama** Cloud Explorer'da kutusu.

![Cloud Explorer'da kaynakları bulma](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Hello karakter girerken **arama** kutusu, bu karakterler karşılayan kaynakları hello kaynak ağacında görünür.
