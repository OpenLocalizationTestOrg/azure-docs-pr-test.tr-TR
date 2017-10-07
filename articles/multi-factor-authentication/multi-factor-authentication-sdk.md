---
title: "özel uygulamalar için aaaMFA Yazılım Geliştirme Seti | Microsoft Docs"
description: "Bu makalede, nasıl Azure MFA SDK tooenable iki aşamalı doğrulamayı özel uygulamalarınız için toodownload ve kullanım hello gösterir."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Yapı multi-Factor Authentication özel uygulamalar (SDK)

Azure AD kiracınıza uygulamaların işlem işlemler veya oturum açma hello iki aşamalı doğrulamayı doğrudan yapı hello Azure çok faktörlü kimlik doğrulaması Yazılım Geliştirme Seti (SDK) sağlar.

Merhaba multi-Factor Authentication SDK'sı, C#, Visual Basic (.NET), Java, Perl, PHP ve Ruby için kullanılabilir. Merhaba SDK iki aşamalı doğrulamayı çevresinde ince bir sarmalayıcı sağlar. Açıklamalı kaynak kodu dosyaları, örneğin dosyaları ve ayrıntılı bir benioku dosyası da dahil olmak üzere, kodunuzu toowrite gereken her şeyi içerir. Her SDK ayrıca bir sertifika ve benzersiz tooyour çok faktörlü kimlik doğrulama sağlayıcısı hareketler şifreleme için özel anahtarı içerir. Bir sağlayıcı sahip olduğu sürece, gerektiği kadar çok dil ve biçimleri hello SDK indirebilirsiniz.

Merhaba multi-Factor Authentication SDK'sı API'lerini hello Hello yapısını basit bir işlemdir. Tek işlev hello çok faktörlü seçeneği parametreleri (gibi doğrulama modu) ve kullanıcı verilerini (Merhaba telefon numarası toocall veya gibi hello PIN numarası toovalidate) ile tooan API çağrısı yapın. Hello API'leri Çevir hello işlev çağrısı web hizmetleri istekleri toohello uygulamasına bulut tabanlı Azure çok faktörlü kimlik doğrulama hizmeti. Tüm çağrılar her SDK'da bulunan başvuru toohello özel sertifika eklemeniz gerekir.

Azure Active Directory'de kayıtlı erişim toousers Hello API'leri sahip değil çünkü bir dosya veya veritabanı kullanıcı bilgilerini sağlamanız gerekir. Ayrıca, hello API'leri sağlamaz kayıt ya da kullanıcı yönetimi özellikleri, yani toobuild gerekiyor uygulamanıza bu işlemler.

> [!IMPORTANT]
> toodownload SDK Merhaba, Azure MFA, AAD Premium veya EMS lisansları olsa bile toocreate Azure multi-Factor Auth sağlayıcısı gerekir. Bu amaç için Azure multi-Factor Auth sağlayıcısı oluşturmak ve lisansları zaten varsa, emin toocreate hello sağlayıcısı hello sahip olun **etkin kullanıcı başına** modeli. Ardından, hello Azure MFA, Azure AD Premium veya EMS lisansları içeren hello sağlayıcısı toohello dizini bağlayın. Bu yapılandırma hello sahip olduğunuz lisans hello sayısından SDK kullanarak daha fazla benzersiz kullanıcı varsa, yalnızca faturalandırılır olmasını sağlar.


## <a name="download-hello-sdk"></a>Merhaba SDK yükle
Hello Azure çok faktörlü SDK'sını indirme gerektiren bir [Azure multi-Factor Auth sağlayıcısı](multi-factor-authentication-get-started-auth-provider.md).  Azure MFA, Azure AD Premium veya Enterprise Mobility Suite lisansları ait olsa bile bu tam Azure aboneliği gerektirir.  toodownload hello SDK, toohello çok faktörlü yönetim portalına gidin. Merhaba portal ya da hello multi-Factor Auth sağlayıcısı doğrudan yönetme veya hello tıklatarak ulaşabilirsiniz **"Git toohello portalı"** hello MFA hizmet ayarları sayfasında bağlantı.

### <a name="download-from-hello-azure-classic-portal"></a>Hello Klasik Azure Portalı ' indirin
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) yönetici olarak.
2. Merhaba solda seçin **Active Directory**.
3. Merhaba Active Directory sayfasında hello üst seçin en **çok faktörlü kimlik doğrulama sağlayıcıları**
4. Merhaba altındaki seçin **Yönet**. Yeni bir sayfa açılır.
5. Merhaba, hello altındaki sol tıklayın **SDK**.
   <center>![İndirme](./media/multi-factor-authentication-sdk/download.png)</center>
6. İstediğiniz bir hello ilişkili indirme bağlantıları tıklatın hello dili seçin.
7. Merhaba indirmeyi kaydedin.

### <a name="download-from-hello-service-settings"></a>Merhaba hizmet ayarlarını indirme
1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) yönetici olarak.
2. Merhaba solda seçin **Active Directory**.
3. Azure AD örneğinize çift tıklayın.
4. Merhaba üst tıklatın adresindeki **Yapılandır**
5. Çok faktörlü kimlik doğrulaması altında seçin **hizmet ayarlarını Yönet**
   ![indirin](./media/multi-factor-authentication-sdk/download2.png)
6. Merhaba ekranında hello altında Hello Hizmetleri ayarları sayfasında, tıklatın **Git toohello portal**. Yeni bir sayfa açılır.
   ![İndir](./media/multi-factor-authentication-sdk/download3a.png)
7. Merhaba, hello altındaki sol tıklayın **SDK**.
8. İstediğiniz bir hello ilişkili indirme bağlantıları tıklatın hello dili seçin.
9. Merhaba indirmeyi kaydedin.

## <a name="whats-in-hello-sdk"></a>Hello nedir SDK
Merhaba SDK hello aşağıdaki öğeleri içerir:

* **BENİOKU**. Nasıl toouse Merhaba çok faktörlü kimlik doğrulaması API'leri yeni veya var olan bir uygulamada açıklanmaktadır.
* **Kaynak dosyaları** çok faktörlü kimlik doğrulaması
* **İstemci sertifikası** toocommunicate hello çok faktörlü kimlik doğrulama hizmeti ile kullanma
* **Özel anahtarı** hello sertifika için
* **Çağrı sonuçları.** Arama sonuç kodları listesi. tooopen bu dosya, bir uygulama, WordPad gibi biçimlendirme metinle kullanın. Kullanım hello sonuç kodları tootest çağırın ve çok faktörlü kimlik doğrulaması hello uyarlamasını uygulamanızda sorun giderme. Kimlik doğrulama durum kodları değiller.
* **Örnekler.** Temel çalışma uygulamasını çok faktörlü kimlik doğrulaması için örnek kod.

> [!WARNING]
> Merhaba istemci sertifikası, özellikle sizin için oluşturulan benzersiz bir özel sertifikasıdır. Paylaşım değil veya bu dosyayı kaybedersiniz. Bu anahtar tooensuring hello güvenliğinizi hello multi-Factor Authentication hizmetiyle, iletişimin olur.

## <a name="code-sample"></a>Kod örneği
Bu kod örneği, nasıl hello Azure multi-Factor Authentication SDK'sı tooadd Standart mod sesli toouse hello API'leri çağırmak doğrulama tooyour uygulama gösterir. Kullanıcı yanıt tooby hello # tuşuna basarak hello bir telefon çağrısı standart moddur.

Bu örnek, C# sunucu tarafı mantığı ile temel bir ASP.NET uygulaması hello C# .NET 2.0 multi-Factor Authentication SDK kullanır, ancak diğer dillerde hello işlemi benzer. Merhaba SDK kaynak dosyaları, değil yürütülebilir dosyaları, içerdiğinden hello dosyaları oluşturmak ve bunları başvuru veya doğrudan uygulamanızda içermiyor.

> [!NOTE]
> Çok faktörlü kimlik doğrulamasını yaparken, hello ek yöntemleri (telefon araması veya kısa mesaj) ikincil veya üçüncül doğrulama toosupplement birincil kimlik doğrulama yöntemi (kullanıcı adı ve parola) kullanın. Bu yöntemler, birincil kimlik doğrulama yöntemi olarak tasarlanmamıştır.

### <a name="code-sample-overview"></a>Kod örnek genel bakış
Bu örnek kod basit bir web demo uygulaması için bir telefon çağrısı # anahtarı yanıtı tooverify hello kullanıcı kimlik doğrulaması ile kullanır. Bu telefon görüşmesi faktörü çok faktörlü kimlik doğrulaması Standart modu olarak bilinir.

Merhaba istemci-tarafı kodu tüm çok faktörlü kimlik doğrulaması özgü öğeleri içermez. Merhaba ek kimlik doğrulama faktörleri hello birincil kimlik doğrulaması bağımsız olduğundan, oturum açma hello varolan arabirimi değiştirmeden ekleyebilirsiniz. hello multi-Factor SDK API'leri Hello hello kullanıcı deneyimini özelleştirmesini sağlar, ancak, toochange herhangi bir şey hiç gerekmeyebilir.

Merhaba sunucu tarafı kodu, adım 2'de Standart mod kimlik doğrulaması ekler. Standart mod doğrulama için gerekli olan hello parametrelere sahip bir PfAuthParams nesnesi oluşturur: kullanıcı adı, telefon numarası ve modu ve hello her çağrıda gereken yolu toohello istemci sertifikası (CertFilePath). PfAuthParams tüm parametreleri tanıtımı için bkz: hello örnek hello SDK dosyasında.

Ardından, hello kod hello PfAuthParams nesnesi toohello pf_authenticate() işlevi iletir. Merhaba dönüş değeri hello başarı veya başarısızlık hello kimlik doğrulamasının gösterir. parametreleri, callStatus ve errorID Merhaba, ek arama sonuç bilgilerini içerir. Merhaba arama sonuç kodları hello arama sonuçları hello SDK dosyasında belgelenmiştir.

Bu en az uygulama birkaç satırda yazılabilir. Ancak, üretim kodunda, daha gelişmiş hata işleme, ek veritabanı kodu ve geliştirilmiş bir kullanıcı deneyimi içerir.

### <a name="web-client-code"></a>Web istemci kodu
Merhaba, web gösteri sayfası için istemci kodu aşağıdadır.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Sunucu Tarafında Çalışan Kod
Sunucu tarafı kodu aşağıdaki hello, çok faktörlü kimlik doğrulaması yapılandırılan ve 2. adımda çalıştırın. Standart mod (MODE_STANDARD) hello # tuşuna basarak bir telefon araması toowhich hello kullanıcı yanıt içindir.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
