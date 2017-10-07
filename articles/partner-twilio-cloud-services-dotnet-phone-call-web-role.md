---
title: "aaaHow toomake bir telefon araması gelen Twilio (.NET) | Microsoft Docs"
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. .NET ile yazılan kod örnekleri."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Nasıl toomake bir telefon görüşmesi Twilio Azure üzerinde bir web rolü kullanma
Bu kılavuz, nasıl toouse Twilio toomake bir web sayfasından bir çağrı Azure üzerinde barındırılan gösterir. Merhaba sonuç uygulaması hello kullanıcı toomake, çağrı hello ekran aşağıdaki gösterildiği gibi numarası ve ileti, verilen hello ile ister.

![Twilio ve ASP.NET kullanarak azure çağrı formu][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Önkoşullar
Toodo hello aşağıdaki gerekir toouse hello kod bu konuda:

1. Twilio hesabı ve kimlik doğrulaması almak hello belirtecine [Twilio konsol][twilio_console]. tooget tarihinde başladı, Twilio, oturum [https://www.twilio.com/try-twilio][try_twilio]. Konumundaki fiyatlandırma değerlendirebilir [http://www.twilio.com/pricing][twilio_pricing]. Merhaba Twilio tarafından sağlanan API hakkında daha fazla bilgi için bkz: [http://www.twilio.com/voice/api][twilio_api].
2. Merhaba eklemek *Twilio .NET kitaplığı* tooyour web rolü. Bkz: **tooadd hello Twilio kitaplıkları tooyour web rolü projesi**, bu konunun devamındaki.

Temel bir oluşturma konusunda bilgi sahibi olmanız gerekir [Azure Web rolü][azure_webroles_get_started].

## <a name="howtocreateform"></a>Nasıl yapılır: arama yapmak için web formu oluşturma
<a id="use_nuget"></a>tooadd hello Twilio kitaplıkları tooyour web rolü projesi:

1. Çözümünüzü Visual Studio'da açın.
2. Sağ **başvurular**.
3. Tıklatın **NuGet paketlerini Yönet**.
4. Tıklatın **çevrimiçi**.
5. Merhaba arama çevrimiçi kutusuna *twilio*.
6. Tıklatın **yükleme** hello Twilio paketinizdeki.

koddan hello nasıl toocreate web form arama yapmak için tooretrieve kullanıcı verileri gösterir. Bu örnekte, bir ASP.NET Web rolü adlı **TwilioCloud** oluşturulur.

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <a id="howtocreatecode"></a>Nasıl yapılır: hello kod toomake hello çağrı oluşturma
Merhaba hello kullanıcı hello form tamamlandığında olarak adlandırılır, aşağıdaki kod, hello çağrı iletisi oluşturur ve hello çağrı oluşturur. Bu örnekte, hello kod hello onclick olay işleyicisini hello düğmesinin hello form üzerinde çalıştırılır. (Twilio hesabı ve kimlik doğrulama belirteci çok atanan hello yer tutucu değerlerini yerine kullanım`accountSID` ve `authToken` aşağıdaki hello kodda.)

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

Merhaba çağrı yapılır ve hello Twilio uç noktası, API sürümü ve hello arama durumu görüntülenir. ekran görüntüsü gösterildiği çıkış çalıştırmak bir örnekten aşağıdaki hello.

![Twilio ve ASP.NET kullanılarak azure çağrı yanıtı][twilio_dotnet_basic_form_output]

TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml]. Hakkında daha fazla bilgi &lt;Say&gt; ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Sonraki adımlar
Bu kod tooshow sağlanan Azure üzerinde ASP.NET web rolünde Twilio kullanarak, temel işlevleri. TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz. Örneğin:

* Bir web formu kullanmak yerine, Azure Blob Depolama veya bir Azure SQL veritabanı örneği toostore telefon numaralarını kullanın ve metin arama. Azure BLOB'ları kullanma hakkında daha fazla bilgi için bkz: [nasıl toouse hello Azure Blob Depolama hizmetine .NET][howto_blob_storage_dotnet]. SQL veritabanı kullanma hakkında daha fazla bilgi için bkz: [nasıl toouse Azure SQL veritabanı .NET uygulamalarında][howto_sql_azure_dotnet].
* Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio hesap Kimliğini ve kimlik doğrulama belirteci hello değerlerde kodlamak formunuz yerine dağıtımınızın yapılandırma ayarları. Merhaba hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].
* Merhaba Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].
* Twilio hakkında daha fazla bilgi [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Ayrıca bkz.
* [Nasıl toouse Twilio azure'dan ses ve SMS özellikleri](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
