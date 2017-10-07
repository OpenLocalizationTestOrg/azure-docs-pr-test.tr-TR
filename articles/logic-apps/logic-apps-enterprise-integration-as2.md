---
title: "B2B Kurumsal tümleştirme - Azure Logic Apps için aaaAS2 iletileri | Microsoft Docs"
description: "Exchange AS2 iletileri Azure Logic Apps ile B2B Kurumsal tümleştirme"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Logic apps ile Kurumsal tümleştirme için Exchange AS2 iletileri

Azure mantıksal uygulamaları için AS2 iletileri değiştirebilir önce AS2 sözleşmesi oluşturun ve bu anlaşma tümleştirme hesabınızı depolamak. Merhaba adımlar şunlardır toocreate bir AS2 sözleşmesi.

## <a name="before-you-start"></a>Başlamadan önce

Gereksinim duyduğunuz hello öğeleri şöyledir:

* Bir [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-accounts.md) , daha önce tanımlanan ve Azure aboneliğinizle ilişkili
* En az iki [ortakları](logic-apps-enterprise-integration-partners.md) , zaten tümleştirme hesabınızda tanımlanır ve hello AS2 niteleyicisi altında yapılandırılmış **iş kimlikleri**

> [!NOTE]
> Bir sözleşme oluşturduğunuzda hello sözleşmesi dosyasında hello içeriği hello anlaşma türüyle eşleşmelidir.    

Çalıştırdıktan sonra [tümleştirme hesap oluşturmak](../logic-apps/logic-apps-enterprise-integration-accounts.md) ve [ortakları eklemek](logic-apps-enterprise-integration-partners.md), aşağıdaki adımları izleyerek bir AS2 sözleşmesi oluşturabilirsiniz.

## <a name="create-an-as2-agreement"></a>AS2 sözleşmesi oluşturma

1.  İçinde toohello oturum [Azure portal](http://portal.azure.com "Azure portal").  

2.  Merhaba sol menüden seçin **daha fazla hizmet**. Merhaba arama kutusuna **tümleştirme** filtre olarak. Merhaba sonuçları listesinden seçmek **tümleştirme hesapları**.

    > [!TIP]
    > Görmüyorsanız, **daha fazla hizmet**, tooexpand hello menü ilk olabilir. Daraltılmış hello menü Hello üstünde seçin **Göster menüsü**.

    !["Tümleştirme hesabı" daha fazla hizmet, "tümleştirme" filtresini seçin.](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. Merhaba, **tümleştirme hesapları** açılır ve select hello tümleştirme hesabını toocreate hello sözleşmesi istediğiniz dikey.
Herhangi bir tümleştirme hesabı görmüyorsanız, [oluşturmak ilk](../logic-apps/logic-apps-enterprise-integration-accounts.md "tümleştirme hesapları hakkında").  

    ![Burada toocreate hello sözleşmesi hello tümleştirme hesabı seçin](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Merhaba seçin **anlaşmaları** döşeme. Anlaşmaları döşeme yoksa, ilk hello kutucuğu ekleyin.

    !["Anlaşmaları" kutucuğunu seçin](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Açılan hello anlaşmaları dikey penceresinde, seçin **Ekle**.

    !["Ekle" yi seçin](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. Altında **Ekle**, girin bir **adı** sözleşmenizi için. İçin **anlaşma türünü**seçin **AS2**. Select hello **ana iş ortağı**, **konak kimliği**, **Konuk iş ortağı**, ve **Konuk kimlik** sözleşmenizi için.

    ![Anlaşma ayrıntılarını sağlayın](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Özellik | Açıklama |
    | --- | --- |
    | Ad |Merhaba anlaşma adı |
    | Anlaşma türü | AS2 olmalıdır |
    | Ana bilgisayar iş ortağı |Bir anlaşma hem konak hem de Konuk iş ortağı gerekir. Merhaba konak ortağı hello sözleşmesi yapılandırır hello kuruluşu temsil eder. |
    | Ana bilgisayar kimliği |Merhaba ana iş ortağı için bir tanımlayıcı |
    | Konuk iş ortağı |Bir anlaşma hem konak hem de Konuk iş ortağı gerekir. Merhaba Konuk ortağı hello konak ortak iş yapmakta hello kuruluşu temsil eder. |
    | Konuk kimlik |Merhaba Konuk iş ortağı için bir tanımlayıcı |
    | Ayarlarını alma |Bu özellikleri anlaşmanın tarafından alınan tooall iletileri geçerlidir. |
    | Gönderme ayarları |Bu özellikleri anlaşmanın tarafından gönderilen tooall iletileri geçerlidir. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Anlaşma tanıtıcıları iletileri nasıl alınan yapılandırma

Merhaba sözleşmesi özelliklerini ayarladıysanız, bu anlaşmanın nasıl tanımlar ve bu anlaşma ile ortaktan alınan gelen iletileri işleme yapılandırabilirsiniz.

1.  Altında **Ekle**seçin **alma ayarı**.
Bu özellikleri sözleşmenizi iletiler birlikte alış verişleri hello ortağıyla göre yapılandırın. Özellik açıklamaları için bu bölümdeki hello tablosuna bakın.

    !["Alma ayarlarını" yapılandırma](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. İsteğe bağlı olarak, gelen iletileri hello özelliklerini seçerek geçersiz kılabilirsiniz **ileti özelliklerini geçersiz kılma**.

3. Tüm gelen iletileri toobe toorequire imzalı, seçin **ileti imzalanmasını**. Merhaba gelen **sertifika** listesinde, var olan seçin [Konuk iş ortağı ortak sertifika](../logic-apps/logic-apps-enterprise-integration-certificates.md) karışılama iletileri hello imza doğrulama. Veya, yoksa, hello sertifika oluşturun.

4.  şifrelenmiş, tüm gelen iletileri toobe toorequire seçin **ileti şifrelenir**. Merhaba gelen **sertifika** listesinde, var olan seçin [ana iş ortağı özel sertifika](../logic-apps/logic-apps-enterprise-integration-certificates.md) gelen iletilerin şifresini çözmek üzere. Veya, yoksa, hello sertifika oluşturun.

5. Sıkıştırılmış, toorequire iletileri toobe seçin **iletisi sıkıştırılmış**.

6. toosend bir zaman uyumlu değerlendirme bildirim iletisi (MDN) alınan iletilerin seçin **Gönder MDN**.

7. toosend imzalı MDNs alınan iletiler için select **gönderme imzalı MDN**.

8. alınan iletilerin zaman uyumsuz MDNs toosend seçin **gönderme zaman uyumsuz MDN**.

9. Bitirdikten sonra emin toosave ayarlarınızı seçerek olun **Tamam**.

Şimdi sözleşmenizi hazır toohandle gelen ayarları seçili tooyour uygun iletileri.

| Özellik | Açıklama |
| --- | --- |
| İleti özelliklerini geçersiz kılma |Alınan iletilerin özelliklerinde geçersiz kılınabilir gösterir. |
| İletinin imzalanmış olması gerekir |Dijital olarak imzalanmış iletileri toobe gerektirir. Merhaba Konuk iş ortağı ortak sertifika imza doğrulaması için yapılandırın.  |
| İletinin şifrelenmiş olması gerekir |Şifrelenmiş iletileri toobe gerektirir. Olmayan şifrelenmiş iletileri reddedilir. Hello iletilerin şifresini çözmek üzere hello ana iş ortağı özel sertifika yapılandırın.  |
| İletinin sıkıştırılmış olması gerekir |Sıkıştırılmış iletileri toobe gerektirir. Olmayan sıkıştırılmış iletiler reddedilir. |
| MDN metin |Merhaba varsayılan ileti değerlendirme bildirim (MDN) toobe toohello ileti gönderen gönderdi. |
| MDN Gönder |Gönderilen MDNs toobe gerektirir. |
| İmzalı MDN Gönder |İmzalı MDNs toobe gerektirir. |
| MIC algoritması |İletileri imzalamak için hello algoritması toouse seçin. |
| Zaman uyumsuz MDN Gönder | Zaman uyumsuz olarak gönderilen iletileri toobe gerektirir. |
| URL | Burada toosend hello MDNs hello URL'sini belirtin. |

## <a name="configure-how-your-agreement-sends-messages"></a>Nasıl sözleşmenizi iletileri gönderir yapılandırın

Bu anlaşma nasıl tanımlar ve bu anlaşma ile tooyour ortaklarının gönderdiği giden iletilerini işleme yapılandırabilirsiniz.

1.  Altında **Ekle**seçin **gönderme ayarları**.
Bu özellikleri sözleşmenizi iletiler birlikte alış verişleri hello ortağıyla göre yapılandırın. Özellik açıklamaları için bu bölümdeki hello tablosuna bakın.

    ![Merhaba "Gönderme ayarları" özelliklerini ayarla](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend imzalı iletiler tooyour iş ortağı, select **ileti imzalamayı etkinleştirmek**. Merhaba iletilerinde hello imzalama **MIC algoritması** listesi, select hello *ana iş ortağı özel sertifika MIC algoritması*. Ve hello **sertifika** listesinde, var olan seçin [ana iş ortağı özel sertifika](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. toosend şifrelenmiş iletileri toohello iş ortağı, select **etkinleştirmek ileti şifreleme**. Merhaba hello iletileri şifrelemek için **şifreleme algoritması** listesi, select hello *Konuk iş ortağı ortak sertifika algoritması*.
Ve hello **sertifika** listesinde, var olan seçin [Konuk iş ortağı ortak sertifika](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. toocompress selamlama iletisine, select **ileti sıkıştırmayı etkinleştir**.

5. toounfold hello HTTP content-type üstbilgisi tek bir satır, select INTO **Unfold HTTP üstbilgileri**.

6. tooreceive hello için zaman uyumlu MDNs gönderilen iletiler, select **isteği MDN**.

7. tooreceive imzalı MDNs için hello gönderilen iletiler, select **isteği imzalı MDN**.

8. tooreceive hello için zaman uyumsuz MDNs gönderilen iletiler, select **isteği zaman uyumsuz MDN**. Bu seçeneği seçerseniz, burada toosend hello için MDNs hello URL'sini girin.

9. toorequire-inkar edilemez makbuz seçin **etkinleştirmek NRR**.  

10. toospecify algoritması biçimi toouse hello MIC içinde veya üstbilgileri hello AS2 ileti veya MDN, giden hello imzalama seçin **SHA2 algoritması biçimi**.  

11. Bitirdikten sonra emin toosave ayarlarınızı seçerek olun **Tamam**.

Seçili tooyour ayarları uygun iletileri Giden hazır toohandle sözleşmenizi sunulmuştur.

| Özellik | Açıklama |
| --- | --- |
| İleti imzalama etkinleştir |İmzalı hello anlaşma toobe gönderilen tüm iletiler gerektirir. |
| MIC algoritması |iletileri imzalamak için algoritma toouse hello. Merhaba ana iş ortağı özel sertifika MIC algoritması Merhaba iletileri imzalamak için yapılandırır. |
| Sertifika |İletileri imzalamak için hello sertifika toouse seçin. Merhaba iletileri imzalamak için hello ana iş ortağı özel sertifika yapılandırır. |
| İleti şifreleme etkinleştir |Bu anlaşma gönderilen tüm iletiler şifrelenmesi gerektirir. Merhaba iletileri şifrelemek için hello Konuk iş ortağı ortak sertifika algoritması yapılandırır. |
| Şifreleme algoritması |İleti şifreleme için şifreleme algoritması toouse hello. Merhaba iletileri şifrelemek için hello Konuk iş ortağı ortak sertifika yapılandırır. |
| Sertifika |Merhaba sertifika toouse tooencrypt iletileri. Merhaba iletileri şifrelemek için hello Konuk iş ortağı özel sertifika yapılandırır. |
| İleti sıkıştırmayı etkinleştir |Bu anlaşma gönderilen tüm iletiler sıkıştırılması gerektirir. |
| HTTP üstbilgileri unfold |Merhaba HTTP content-type üstbilgisi tek bir satır üzerine yerleştirir. |
| İstek MDN |Bu anlaşma gönderilen tüm iletiler için bir MDN gerektirir. |
| İmzalı MDN isteği |Toobe imzalı toothis sözleşmesi gönderilen tüm MDNs gerektirir. |
| Zaman uyumsuz MDN isteği |Zaman uyumsuz MDNs gönderilen toobe toothis sözleşmesi gerektirir. |
| URL |Burada toosend hello MDNs hello URL'sini belirtin. |
| NRR etkinleştir |İnkar edilemez makbuz (NRR) hello verileri kanıt sağlar iletişimi özniteliği olarak ele gibi alındı gerektirir. |
| SHA2 algoritması biçimi |Merhaba MIC veya giden üstbilgiler hello AS2 ileti veya MDN hello imzalama algoritması biçimi toouse seçin |

## <a name="find-your-created-agreement"></a>Oluşturulan sözleşmenizi Bul

1.  Merhaba üzerinde anlaşma özelliklerinizi ayarlama işlemini tamamladıktan sonra **Ekle** dikey penceresinde, seçin **Tamam** toofinish sözleşmesi ve dönüş tooyour tümleştirme hesabı dikey oluşturma.

    Yeni eklenen sözleşmenizi artık görünür, **anlaşmaları** listesi.

2.  Ayrıca, tümleştirme hesabına genel bakış sözleşmelerinizi görüntüleyebilirsiniz. Tümleştirme hesabı dikey penceresinde, seçin **genel bakış**seçeneğini belirleyip hello **anlaşmaları** döşeme. 

    ![Tüm Anlaşmalar "Anlaşmaları" döşeme tooview seçin](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Görünüm hello swagger
Merhaba bkz [ayrıntıları swagger](/connectors/as2/). 

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Enterprise Integration Pack hakkında daha fazla bilgi](logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")  
