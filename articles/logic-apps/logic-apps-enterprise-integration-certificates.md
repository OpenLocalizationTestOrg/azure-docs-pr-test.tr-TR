---
title: Enterprise Integration Pack aaaUsing sertifikalarla | Microsoft Docs
description: "Enterprise Integration Pack Merhaba ile nasıl toouse sertifikaları öğrenin | Azure mantıksal uygulamaları"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Sertifikalar ve Enterprise Integration Pack hakkında bilgi edinin
## <a name="overview"></a>Genel Bakış
Enterprise Integration sertifikaları toosecure B2B iletişimleri kullanır. Enterprise Integration uygulamalarınızda iki sertifika türünü kullanarak şunları yapabilirsiniz:

* Ortak Sertifikalar, sertifika yetkilisinden (CA) satın alınması gerekir.
* Özel sertifikaları kendiniz uygulayabilirsiniz. Bu sertifikalar bazen başvurulan tooas otomatik olarak imzalanan sertifikalar.

## <a name="what-are-certificates"></a>Sertifikalar nelerdir?
Sertifikalar elektronik iletişimin hello katılımcıları hello kimliğini doğrulamak ve ayrıca elektronik iletişimleri güvenli dijital belgelerdir.

## <a name="why-use-certificates"></a>Sertifikaları neden kullanılır?
Bazen B2B iletişimleri gizli tutulması gerekir. Enterprise Integration sertifikaları toosecure bu iletişimler iki yolla kullanır:

* İletileri Merhaba içeriğine şifreleyerek
* İletileri imzalamak tarafından  

## <a name="upload-a-public-certificate"></a>Ortak sertifikasını karşıya yükle

toouse bir *ortak sertifika* B2B özellikleriyle logic apps içinde ilk tooupload hello sertifika tümleştirme hesabınızda gerekir.  

Bir sertifika yükledikten sonra güvenli B2B iletilerinizi hello özelliklerini tanımladığınızda kullanılabilir toohelp olan [anlaşmaları](logic-apps-enterprise-integration-agreements.md) oluşturduğunuz.  

Merhaba toohello Azure portalında oturum sonra ortak sertifikalarınızı tümleştirme hesabınızda karşıya yükleme için ayrıntılı adımlar şunlardır:

1. Seçin **daha fazla hizmet** ve girin **tümleştirme** hello filtre arama kutusuna. Seçin **tümleştirme hesapları** hello sonuçları listesinden     
![Gözat seçin](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Hello tümleştirme hesabı toowhich tooadd hello sertifika istediğinizi seçin.  
![Merhaba tümleştirme hesabı toowhich tooadd hello sertifika istediğiniz seçin](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Select hello **sertifikaları** döşeme.  
![Select hello sertifikaları döşeme](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. Merhaba, **sertifikaları** açar, select hello dikey **Ekle** düğmesi.   
![Merhaba Ekle düğmesini seçin](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Girin bir **adı** sertifika ve ardından hello sertifika türü olarak **ortak** gelen hello açılır.  
6. Select hello klasör simgesine hello hello sağ tarafındaki **sertifika** metin kutusu. Merhaba dosya seçiciyi oturum açtığında, bulun ve tooupload tooyour tümleştirme hesabını istediğiniz hello sertifika dosyasını seçin.
7. Merhaba sertifikayı seçin ve ardından **Tamam** hello dosya Seçici. Bu doğrular ve hello sertifika tooyour tümleştirme hesabı yükler.
8. Son olarak, üzerinde hello geri **sertifika Ekle** dikey penceresinde, select hello **Tamam** düğmesi.  
![Merhaba Tamam düğmesini seçin](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Select hello **sertifikaları** döşeme. Merhaba sertifika yeni eklenen görmeniz gerekir.  
![Merhaba yeni sertifika bakın](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Özel bir sertifika karşıya yükle

toouse bir *özel sertifika* B2B özellikleriyle logic apps içinde aşağıdaki adımları alma hello tarafından özel sertifika tooyour tümleştirme hesabı karşıya yükleyebilirsiniz

1. [Özel anahtar tooKey kasası karşıya](../key-vault/key-vault-get-started.md "anahtar kasası hakkında bilgi edinin") ve sağlayan bir **anahtar adı** 
   
   > [!TIP]
   > Anahtar kasası Logic Apps tooperform işlemleri yetkilendirmeniz gerekir. Merhaba aşağıdaki PowerShell komutunu kullanarak erişim toohello Logic Apps hizmet sorumlusu verebilirsiniz:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Merhaba önceki adımı ayırdıktan sonra bir özel sertifika toointegration hesabı ekleyin.

Aşağıdaki hello toohello Azure portalında oturum sonra özel sertifikalarınızı tümleştirme hesabınızda karşıya yükleme için ayrıntılı adımlar:  
 
1. Tooadd hello sertifika istediğiniz ve seçin hello hello tümleştirme hesap toowhich seçin **sertifikaları** döşeme.  
![Select hello sertifikaları döşeme](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. Merhaba, **sertifikaları** açar, select hello dikey **Ekle** düğmesi.   
![Merhaba Ekle düğmesini seçin](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Girin bir **adı** sertifika ve select hello sertifika türü olarak **özel** gelen hello açılır.   
4. Merhaba klasör simgesine hello hello sağ tarafındaki seçin **sertifika** metin kutusu. Merhaba dosya seçiciyi oturum açtığında, tooupload tooyour tümleştirme hesabını istediğiniz hello karşılık gelen ortak sertifika bulun.   
   
   > [!Note]
   > Özel bir sertifika eklenirken karşılık gelen ortak tooadd sertifika tooshow içinde önemlidir [AS2 sözleşmesi](logic-apps-enterprise-integration-as2.md) gönderip ayarları imzalama ve karışılama iletileri şifrelemek için.
   > 
   >   

5. Select hello **kaynak grubu**, **anahtar kasası**, **anahtar adı** ve select hello **Tamam** düğmesi.  
![Sertifika Ekle](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Select hello **sertifikaları** döşeme. Merhaba sertifika yeni eklenen görmeniz gerekir.
![Merhaba yeni sertifika bakın](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [B2B sözleşmesi oluşturma](logic-apps-enterprise-integration-agreements.md)  
* [Anahtar kasası hakkında daha fazla bilgi](../key-vault/key-vault-get-started.md "anahtar kasası hakkında bilgi edinin")  

