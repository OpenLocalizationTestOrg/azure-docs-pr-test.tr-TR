---
title: "Ekleme veya Azure yönetici abonelik rolleri değiştirme | Microsoft Docs"
description: "Azure ortak yönetici, Hizmet Yöneticisi ve Hesap Yöneticisi ekleme veya değiştirme açıklar"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: da5995535d42ed52772cb09e0f4da51bbf878748
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-the-subscription-or-services"></a>Ekleme veya abonelik ya da hizmetleri yönetmek Azure yönetici rollerini değiştirme
Azure aboneliğiniz yönetir veya aboneliğinizde kullanılan Azure hizmetlerini yöneten Azure yönetici değiştirebilirsiniz. Azure faturalama bilgilerini görüntülemek ve Aboneliklerini yönetmek için oturum gerekir [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index) hesap yöneticisi olarak. 

## <a name="add-an-admin-for-a-subscription"></a>Bir abonelik için bir yönetici ekleme
Azure portalında veya Klasik Azure portalındaki Azure yönetici ekleyebilirsiniz.

**Azure portal**

Birisi bir abonelik Azure portalında yönetici olarak eklemek için bunları sahip rolünü verin. Sahip rolü yalnızca size atanan abonelik kaynakları yönetebilir. Diğer aboneliklere erişim ayrıcalığına sahip değil. Eklediğiniz aracılığıyla sahipleri [Azure portal](https://portal.azure.com) kaynağında yönetemez [Klasik Azure portalı](https://manage.windowsazure.com).

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Hub menüsünde seçin **abonelik** > *erişmek için yönetim istediğiniz abonelik*.

    ![Seçili abonelik gösteren ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Abonelik dikey penceresinde, seçin **erişim denetimi (IAM)**.
4. Seçin **ekleme** > **rol** > **sahibi**. Sahibi olarak eklemek istediğiniz kullanıcıyı seçin ve ardından istediğiniz kullanıcının e-posta adresini yazın **kaydetmek**.

    ![Seçili sahip rolünü gösteren ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Ortak yönetici sahip hesabı eklemek isteyip istemediğinizi **erişim denetimi (IAM)** sayfasında, kullanıcıyı sağ tıklatın ve ardından **ortak yönetici olarak Ekle**. Bu özellik artık kullanılabilir [Azure Önizleme portalı](https://preview.portal.azure.com/). 

     ![Ortak yönetici ekler ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Kullanıcının Azure hizmetleri yönetmek gerekirse "Sahip" kullanıcı ortak yönetici olarak eklemeniz gerekir [Klasik Azure portalı](https://manage.windowsazure.com/).

    Ortak yönetici izni kaldırmak için "ortak Yöneticisi" kullanıcı sağ tıklayın ve ardından **kaldırmak ortak yönetici**.

    ![Ortak yönetici kaldırır ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Klasik Azure Portalı**

1. [Klasik Azure portalında](https://manage.windowsazure.com/) oturum açın.
2. Gezinti bölmesinde seçin **ayarları**> **Yöneticiler**> **Ekle**. </br>

    ![Alma için Ekle düğmesini gösteren ekran görüntüsü](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Ortak yönetici olarak ekleme ve erişmek için ortak yönetici istediğiniz aboneliği seçmek istediğiniz kişinin e-posta adresini yazın.</br>

    ![Seçili abonelik gösteren ekran görüntüsü ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Aşağıdaki e-posta adresi, bir ortak yönetici eklenebilir:

* **Microsoft Account** (eskiden Windows Live kimliği) </br>
  İçin tüm tüketiciye yönelik Microsoft ürünlerini oturum açma ve bulut hizmetlerine (Hotmail) Outlook ve Skype (MSN), OneDrive, Windows Phone ve Xbox LIVE gibi Microsoft Account kullanabilirsiniz.
* **Kurumsal hesap**</br>
  Bir kurumsal hesap Azure Active Directory altında oluşturulan hesaptır. Kurumsal hesap adresi bu biçime sahiptir:

    Kullanıcı @&lt;etki alanınızın&gt;. onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Bir aboneliği için Hizmet Yöneticisi değiştirme
Yalnızca Hesap Yöneticisi bir aboneliği için Hizmet Yöneticisi değiştirebilirsiniz.

1. Oturum [Azure hesap Merkezi](https://account.windowsazure.com/subscriptions) Hesap Yöneticisi kullanarak.
2. Değiştirmek istediğiniz aboneliği seçin.
3. Sağ tarafta seçin **Düzenle abonelik** ayrıntıları. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. İçinde **Hizmet Yöneticisi** kutusuna, yeni Hizmet Yöneticisi'nin e-posta adresi girin. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-the-account-administrator"></a>Hesap Yöneticisi değiştirme
Azure hesabı sahipliğini aktarmak için başka bir hesap için bkz: [bir Azure aboneliği sahipliğini aktarma](billing-subscription-transfer.md).

Silmediğinizden veya hesap yöneticisinin e-posta adresi yeniden adlandırmak, kesinlikle öneririz. Azure hesabı ile beklenmeyen ve istenmeyen davranışı görebilirsiniz. Düzgün mümkün ile oturum açma Azure o hesabı olması, hesabına değişiklik veya bu hesap ile kaynakları yönetme. 

## <a name="check-the-account-administrator-of-the-subscription"></a>Aboneliğin Hesap Yöneticisi denetleyin
Aboneliğiniz hesap yöneticisi olan emin değilseniz, öğrenmek için aşağıdaki adımları kullanın.

  1. [Azure Portal](https://portal.azure.com) oturum açın.
  2. Hub menüsünde seçin **abonelik**.
  3. Denetleyin ve altında aramak istediğiniz aboneliği seçin **ayarları**.
  4. Seçin **özellikleri**. Aboneliğin Hesap Yöneticisi görüntülenen **Hesap Yöneticisi** kutusu.  

## <a name="types-of-azure-admin-accounts"></a>Azure Yönetici hesap türleri
 Hesap Yöneticisi, Hizmet Yöneticisi ve ortak yönetici üç Microsoft Azure yönetici rolleri türleridir. Aşağıdaki tabloda, bu üç yönetici rolleri arasındaki farkı açıklar.

| Yönetim rolü | Sınır | Açıklama |
| --- | --- | --- |
| Hesap Yöneticisi (AA) |Azure hesabı başına 1 |Bu kaydolup veya Azure aboneliklerinin satın aldınız ve erişim yetkisi kişidir [hesap Merkezi'nde](https://account.windowsazure.com/Home/Index) ve çeşitli yönetim görevlerini gerçekleştirebilirsiniz. Bunlar, abonelikleri oluşturma, aboneliklerinizi iptal edin, bir abonelik için faturalama değiştirin ve Hizmet Yöneticisi değiştirmek çalışabilme içerir. |
| Hizmet Yöneticisi (SA) |Azure abonelik başına 1 |Bu rol hizmetleri yönetmeye yetkilidir [Azure portal](https://portal.azure.com). Varsayılan olarak, yeni bir abonelik için Hesap Yöneticisi ayrıca hizmet yöneticisidir. |
| Ortak yönetici (CA) [Klasik Azure portalı](https://manage.windowsazure.com) |Abonelik başına 200 |Bu rol Hizmet Yöneticisi ile aynı erişim ayrıcalıklarına sahiptir, ancak aboneliklerin Azure dizinleriyle ilişkisini değiştiremez. |

Azure Active Directory rol tabanlı erişim denetimi (RBAC), kullanıcıların birden çok rol eklenmesine izin verir. Daha fazla bilgi için bkz: [Azure Active Directory rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Sınırlamalar ve yönetici hesapları için kısıtlamalar
* Her abonelik, Azure AD dizini (olarak da bilinen varsayılan dizin) ile ilişkilidir. Abonelik ile ilişkili varsayılan dizini bulmak için Git [Klasik Azure portalı](https://manage.windowsazure.com/)seçin **ayarları** > **abonelikleri**. Varsayılan dizini bulmak için abonelik Kimliğini denetleyin.
* Bir Microsoft Account oturum açtıysanız, ortak yönetici olarak diğer Microsoft Accounts veya varsayılan dizin içindeki kullanıcılar yalnızca ekleyebilirsiniz.
* Bir kurumsal hesapla oturum açtıysanız, ortak yönetici olarak, kuruluşunuzdaki diğer Kurumsal hesaplar ekleyebilirsiniz. Örneğin, abby@contoso.com ekleyebilirsiniz bob@contoso.com Hizmet Yöneticisi veya ortak yönetici olarak ekleyemezsiniz, ancak john@notcontoso.com sürece john@notcontoso.com varsayılan dizindir. Kuruluş hesaplarıyla oturum imzalı kullanıcılar Hizmet Yöneticisi veya ortak yönetici Microsoft Account kullanıcıları eklemeye devam edebilirsiniz.
* Azure için bir kuruluş hesabı ile oturum açmak mümkündür, Hizmet Yöneticisi ve ortak yönetici hesabı gereksinimleri değişiklikler şunlardır:

  | Yönteminde oturum | Microsoft Account veya kullanıcıların varsayılan dizin içindeki CA veya SA olarak eklensin mi? | CA veya SA olarak aynı kuruluşta kuruluş hesabı eklensin mi? | Farklı bir kuruluşta CA veya SA olarak kuruluş hesabı eklensin mi? |
  | --- | --- | --- | --- |
  |  Microsoft Hesabı |Evet |Hayır |Hayır |
  |  Kurumsal Hesap |Evet |Evet |Hayır |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Kaynak erişim denetimi ve Active Directory hakkında daha fazla bilgi edinin
* Microsoft Azure'da kaynak erişiminin nasıl denetlendiğini hakkında daha fazla bilgi için bkz: [azure'da kaynak erişimini anlama](../active-directory/active-directory-understanding-resource-access.md).
* Azure Active Directory hakkında daha fazla bilgi için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](../active-directory/active-directory-how-subscriptions-associated-directory.md) ve [Azure Active Directory'de yönetici rolleri atama](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) hızla çözümlenen sorunu almak için.
