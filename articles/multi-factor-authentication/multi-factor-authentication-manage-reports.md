---
title: "Azure MFA için aaaAccess ve kullanım raporları | Microsoft Docs"
description: "Bu, nasıl toouse hello Azure çok faktörlü kimlik doğrulama özelliği - raporları açıklar."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a>Azure multi-Factor Authentication raporlarında
Azure çok faktörlü kimlik doğrulaması ve kuruluşunuz tarafından kullanılan çeşitli raporlar sağlar. Bu raporlar hello multi-Factor Authentication Yönetim Portalı erişilebilir. Merhaba, hello kullanılabilir raporlar listesi aşağıdadır:

| Rapor | Açıklama |
|:--- |:--- |
| Kullanım |Merhaba kullanım raporları bilgileri görüntüler genel kullanımı, kullanıcı özeti ve kullanıcı ayrıntıları. |
| Sunucu durumu |Bu rapor, çok faktörlü kimlik doğrulama için hesabınızla ilişkili sunucularını hello durumunu görüntüler. |
| Engellenmiş kullanıcı geçmişi |Bu raporlar istekleri tooblock hello geçmişini göster kullanıcı veya engelini kaldırma. |
| Atlanmış kullanıcı geçmişi |Bir kullanıcının telefon numarası için çok faktörlü kimlik doğrulama isteklerini toobypass Hello geçmişini gösterir. |
| Sahtekarlık Uyarısı |Belirttiğiniz hello tarih aralığı içinde gönderilen sahtekarlık uyarısı geçmişini gösterir. |
| Sıraya alınmış |Sıraya alınan işleme ve durumlarını listeler raporları. Merhaba rapor tamamlandığında, bir bağlantı toodownload veya Görünüm hello rapor sağlanır. |

## <a name="view-reports"></a>Raporları görüntüleme
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol tarafta, Active Directory'yi seçin.
3. Kimlik doğrulama sağlayıcıları kullanmadığınıza bağlı olarak bu iki seçenekten birini izleyin:
   * **Seçenek 1**: Merhaba çok faktörlü kimlik doğrulama sağlayıcıları sekmesini tıklatın. MFA sağlayıcınızı seçin ve hello tıklatın **Yönet** hello altındaki düğmesi.
   * **Seçenek 2**: dizin ve Git toohello seçin **yapılandırma** sekmesi. Merhaba çok faktörlü kimlik doğrulaması bölümü altında seçin **hizmet ayarlarını Yönet**. Merhaba MFA Hizmeti Ayarları sayfası Hello altındaki hello Git toohello portal bağlantıyı tıklatın.
4. Hello Azure multi-Factor Authentication Yönetim Portalı'da, hello hello istediğiniz rapor türünü seçin **bir raporu görüntülemek** sol gezinti hello bölümünde.

<center>![Bulut](./media/multi-factor-authentication-manage-reports/report.png)</center>


**Ek Kaynaklar**

* [Kullanıcılar için](end-user/multi-factor-authentication-end-user.md)
* [MSDN'deki Azure çok faktörlü kimlik doğrulaması](https://msdn.microsoft.com/library/azure/dn249471.aspx)
