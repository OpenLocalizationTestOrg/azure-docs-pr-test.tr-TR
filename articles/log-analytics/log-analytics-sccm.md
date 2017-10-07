---
title: Configuration Manager tooLog Analytics aaaConnect | Microsoft Docs
description: "Bu makalede, analiz ve veri çözümleme başlangıç hello adımları tooconnect Configuration Manager tooLog gösterilmektedir."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Configuration Manager tooLog Analytics Bağlan
System Center Configuration Manager tooLog Analytics OMS toosync aygıt koleksiyonu verilerdeki bağlanabilir. Bu veri, Configuration Manager hiyerarşisinden OMS kullanılabilir hale getirir.

## <a name="prerequisites"></a>Ön koşullar

Günlük analizi System Center Configuration Manager geçerli dalı, sürüm 1606 ve üstünü destekler.  

## <a name="configuration-overview"></a>Yapılandırmasına genel bakış
Aşağıdaki adımları hello hello işlem tooconnect Configuration Manager tooLog Analytics özetler.  

1. Hello Azure Yönetim Portalı, Configuration Manager bir Web uygulaması ve/veya Web API uygulaması kaydetmek ve hello istemci kimliği ve istemci gizli anahtarı hello kayıt Azure Active Directory'den sahip olduğundan emin olun. Bkz: [portal toocreate Active Directory Uygulama ve kaynaklarına erişebilir hizmet sorumlusu kullanmak](../azure-resource-manager/resource-group-create-service-principal-portal.md) hakkında ayrıntılı bilgi için bu adımı gerçekleştirmek.
2. Hello Azure Yönetim Portalı'nda [Configuration Manager (Merhaba kayıtlı web uygulaması) izni tooaccess OMS sağlamak](#provide-configuration-manager-with-permissions-to-oms).
3. Yapılandırma Yöneticisi'nde [hello ekleme OMS Bağlantı Sihirbazı'nı kullanarak bir bağlantı ekleyin](#add-an-oms-connection-to-configuration-manager).
4. Yapılandırma Yöneticisi'nde [güncelleştirme hello bağlantı özellikleri](#update-oms-connection-properties) süresi veya kaybolursa hiç hello parola veya istemci gizli anahtarı.
5. Merhaba OMS Portalı'ndan bilgilerle [hello Microsoft Monitoring Agent'ı yükleyip](#download-and-install-the-agent) hello Configuration Manager hizmeti bağlantısı çalıştıran hello bilgisayarda noktası site sistemi rolü. Merhaba aracı Configuration Manager veri tooOMS gönderir.
6. Günlük analizi içinde [koleksiyonları Configuration Manager içinden içe](#import-collections) bilgisayar grupları olarak.
7. Günlük analizi içinde verisinin Yapılandırma Yöneticisi'nden olarak [bilgisayar grupları](log-analytics-computer-groups.md).

Daha fazla bilgiyi, Configuration Manager tooOMS bağlanma hakkında [eşitleme Configuration Manager toohello Microsoft Operations Management Suite verilerden](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Configuration Manager ile izinleri tooOMS girin
Merhaba aşağıdaki yordam hello Azure Yönetim Portalı izinleri tooaccess OMS ile sağlar. Özellikle, hello vermelidir *katkıda bulunan rolü* toousers sipariş tooallow hello kaynak grubunda hello Azure Yönetim Portalı tooconnect Configuration Manager tooOMS.

> [!NOTE]
> OMS Configuration Manager için izinleri belirtmeniz gerekir. Aksi takdirde, Yapılandırma Yöneticisi'nde hello Yapılandırma Sihirbazı'nı kullanırken bir hata iletisi alırsınız.
>
>

1. Açık hello [Azure portal](https://portal.azure.com/) tıklatıp **Gözat** > **günlük analizi (OMS)** tooopen hello günlük analizi (OMS) dikey.  
2. Merhaba üzerinde **günlük analizi (OMS)** dikey penceresinde tıklatın **Ekle** tooopen hello **OMS çalışma** dikey.  
   ![OMS dikey penceresi](./media/log-analytics-sccm/sccm-azure01.png)
3. Merhaba üzerinde **OMS çalışma** dikey penceresinde, aşağıdaki bilgilerle hello sağlayın ve ardından **Tamam**.

   * **OMS çalışma**
   * **Abonelik**
   * **Kaynak grubu**
   * **Konum**
   * **Fiyatlandırma katmanı**  
     ![OMS dikey penceresi](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > Yukarıdaki Hello örnek yeni bir kaynak grubu oluşturur. Yalnızca kullanılan tooprovide Configuration Manager bu örnekte izinleri toohello OMS çalışma ile Merhaba kaynak grubudur.
     >
     >
4. Tıklatın **Gözat** > **kaynak grupları** tooopen hello **kaynak grupları** dikey.
5. Merhaba, **kaynak grupları** dikey penceresinde tooopen hello oluşturduğunuz hello kaynak grubunu tıklatın &lt;kaynak grubu adı&gt; ayarlar dikey penceresi.  
   ![kaynak grubu ayarları dikey](./media/log-analytics-sccm/sccm-azure03.png)
6. Merhaba, &lt;kaynak grubu adı&gt; dikey penceresinde, erişim denetimi (IAM) tooopen hello tıklatın &lt;kaynak grubu adı&gt; kullanıcılar dikey penceresi.  
   ![kaynak grubu kullanıcılar dikey penceresi](./media/log-analytics-sccm/sccm-azure04.png)  
7. Merhaba, &lt;kaynak grubu adı&gt; kullanıcılar dikey penceresi, tıklatın **Ekle** tooopen hello **erişim Ekle** dikey.
8. Merhaba, **erişim Ekle** dikey penceresinde tıklatın **bir rol seçin**seçip hello **katkıda bulunan** rol.  
   ![bir rol seçin](./media/log-analytics-sccm/sccm-azure05.png)  
9. Tıklatın **kullanıcıları eklemek**, hello Configuration Manager kullanıcısını seçin, **seçin**ve ardından **Tamam**.  
   ![kullanıcıları ekleme](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>OMS bağlantısı tooConfiguration Yöneticisi ekleme
Sipariş tooadd bir OMS bağlantısı, Configuration Manager ortamınızı olmalıdır bir [hizmet bağlantı noktası](https://technet.microsoft.com/library/mt627781.aspx) çevrimiçi modu için yapılandırılmış.

1. Merhaba, **Yönetim** çalışma Configuration Manager, select **OMS bağlayıcı**. Merhaba açılır **OMS Bağlantısı Ekleme Sihirbazı'nı**. Seçin **sonraki**.
2. Merhaba üzerinde **genel** eylemleri aşağıdaki hello yaptıktan ve her öğeye ilişkin ayrıntıları sahip sonra seçin onaylayın **sonraki**.

   1. Azure Yönetim Portalı'nda Merhaba, bir Web uygulaması ve/veya Web API uygulaması Configuration Manager kayıtlı ve sahip hello [hello kayıt istemci kimliği](../active-directory/active-directory-integrating-applications.md).
   2. Hello Azure Yönetim Portalı, Azure Active Directory'de hello kayıtlı uygulama için bir uygulama gizli anahtarı oluşturdunuz.  
   3. Hello Azure Yönetim Portalı'da, izni tooaccess OMS hello kayıtlı web uygulaması sağladık.  
      ![Bağlantı tooOMS Sihirbazı genel sayfası](./media/log-analytics-sccm/sccm-console-general01.png)
3. Merhaba üzerinde **Azure Active Directory** ekranında, bağlantı ayarları tooOMS sağlayarak yapılandırmak, **Kiracı** , **istemci kimliği** , ve **istemci gizli anahtar**  seçeneğini belirleyip **sonraki**.  
   ![Bağlantı tooOMS Sihirbazı Azure Active Directory sayfası](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Tüm hello diğer yordamlar başarıyla tamamlanan, hello hakkında bilgi hello **OMS bağlantı yapılandırması** ekranı otomatik olarak bu sayfada görüntülenir. Merhaba bağlantı ayarlarının bilgileri için görünmelidir, **Azure aboneliği** , **Azure kaynak grubu** , ve **Operations Management Suite çalışma alanı**.  
   ![Bağlantı tooOMS Sihirbazı OMS bağlantısı sayfası](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Merhaba Sihirbazı giriş hello bilgileri kullanarak toohello OMS hizmetine bağlanır. OMS ile toosync istediğiniz ve ardından hello cihaz koleksiyonları seçin **Ekle**.  
   ![Koleksiyonları seçin](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Merhaba, bağlantı ayarlarını doğrulayın **Özet** ekran sonra seçin **sonraki**. Merhaba **ilerleme** ekran hello bağlantı durumunu gösterir, ardından gereken **tam**.

> [!NOTE]
> Hiyerarşinizdeki OMS toohello üst katman sitesine bağlanmanız gerekir. OMS tooa tek başına birincil siteye bağlanmak ve sonra bir merkezi yönetim sitesi tooyour ortamı eklerseniz, toodelete olması ve hello yeni hiyerarşi içinde hello OMS bağlantısı oluşturun.
>
>

Configuration Manager tooOMS bağlı sonra eklemek veya koleksiyonları kaldırın ve hello OMS bağlantısı hello özelliklerini görüntüleyin.

## <a name="update-oms-connection-properties"></a>OMS bağlantısı özelliklerini güncelleştir
Bir parola veya istemci gizli anahtarı hiç süresi veya kaybolursa toomanually güncelleştirme hello OMS bağlantısı özellikleri gerekir.

1. Yapılandırma Yöneticisi'nde çok gidin**bulut Hizmetleri** seçeneğini belirleyip **OMS bağlayıcı** tooopen hello **OMS bağlantısı özellikleri** sayfası.
2. Bu sayfada hello tıklatın **Azure Active Directory** tooview sekmesinde, **Kiracı**, **istemci kimliği**, **istemci gizli anahtarı sona erme**. **Doğrulama** , **istemci gizli anahtarı** süresi dolmuşsa.

## <a name="download-and-install-hello-agent"></a>Merhaba aracıyı indirin ve yükleyin
1. Merhaba OMS portalında [indirme hello agent kurulum dosyası OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Yöntemleri tooinstall aşağıdaki hello birini kullanın ve hello Configuration Manager hizmet bağlantı noktası site sistem rolü çalıştıran hello bilgisayarda hello Aracısı yapılandırın:
   * [Kurulumu kullanarak hello aracı yükleme](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Merhaba komut satırını kullanarak hello aracı yükleme](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Azure Otomasyonu'nda DSC kullanarak hello aracı yükleme](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Koleksiyonları İçeri Aktar
OMS bağlantısı tooConfiguration Yöneticisi ekledikten ve hello aracısı yüklü sonra hello Configuration Manager hizmeti bağlantısı çalıştıran hello bilgisayarda noktası site sistemi rolü, hello sonraki adıma tooimport koleksiyonları Yapılandırma Yöneticisi'nden OMS bilgisayar grupları olarak.

Başlangıcından etkinleştirildikten sonra hello koleksiyon üyeliği bilgiler alınır her 3 saat tookeep hello koleksiyon üyelikleri geçerli. Herhangi bir zamanda toodisable başlangıcından seçebilirsiniz.

1. Merhaba OMS portalında tıklatın **ayarları**.
2. Merhaba tıklatın **bilgisayar grupları** sekmesini ve sonra hello **SCCM** sekmesi.
3. Seçin **alma Configuration Manager koleksiyon üyelikleri** ve ardından **kaydetmek**.  
   ![Bilgisayar grupları - SCCM sekmesi](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Yapılandırma Yöneticisi'nden verileri görüntüleme
OMS bağlantısı tooConfiguration Yöneticisi eklenir ve hello Aracısı hello Configuration Manager hizmet bağlantı noktası site sistem rolü çalıştıran hello bilgisayarda yüklü sonra verileri hello aracısından tooOMS gönderilir. Configuration Manager koleksiyonlarınızı OMS içinde görünür [bilgisayar grupları](log-analytics-computer-groups.md). Merhaba hello gruplarından görüntüleyebilirsiniz **Configuration Manager** altında sayfa **bilgisayar grupları** içinde **ayarları**.

Hello koleksiyonları alındıktan sonra koleksiyon üyelikleri kaç bilgisayarlarla algılanan görebilirsiniz. İçe aktarılan koleksiyon hello sayısı de görebilirsiniz.

![Bilgisayar grupları - SCCM sekmesi](./media/log-analytics-sccm/sccm-computer-groups02.png)

Bunlardan herhangi birinin, arama açılır tıklattığınızda hello ya da tümü görüntüleme grupları veya tooeach grubu ait tüm bilgisayarları içeri. Kullanarak [günlük arama](log-analytics-log-searches.md), Configuration Manager veri ayrıntılı analizini başlatabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük arama](log-analytics-log-searches.md) tooview ayrıntılı Configuration Manager verileriniz hakkında bilgi.
