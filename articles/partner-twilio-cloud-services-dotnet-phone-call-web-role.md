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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="eb284-104">Nasıl toomake bir telefon görüşmesi Twilio Azure üzerinde bir web rolü kullanma</span><span class="sxs-lookup"><span data-stu-id="eb284-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="eb284-105">Bu kılavuz, nasıl toouse Twilio toomake bir web sayfasından bir çağrı Azure üzerinde barındırılan gösterir.</span><span class="sxs-lookup"><span data-stu-id="eb284-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="eb284-106">Merhaba sonuç uygulaması hello kullanıcı toomake, çağrı hello ekran aşağıdaki gösterildiği gibi numarası ve ileti, verilen hello ile ister.</span><span class="sxs-lookup"><span data-stu-id="eb284-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Twilio ve ASP.NET kullanarak azure çağrı formu][twilio_dotnet_basic_form]

## <span data-ttu-id="eb284-108"><a name="twilio-prereqs"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="eb284-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="eb284-109">Toodo hello aşağıdaki gerekir toouse hello kod bu konuda:</span><span class="sxs-lookup"><span data-stu-id="eb284-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="eb284-110">Twilio hesabı ve kimlik doğrulaması almak hello belirtecine [Twilio konsol][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="eb284-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="eb284-111">tooget tarihinde başladı, Twilio, oturum [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="eb284-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="eb284-112">Konumundaki fiyatlandırma değerlendirebilir [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="eb284-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="eb284-113">Merhaba Twilio tarafından sağlanan API hakkında daha fazla bilgi için bkz: [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="eb284-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="eb284-114">Merhaba eklemek *Twilio .NET kitaplığı* tooyour web rolü.</span><span class="sxs-lookup"><span data-stu-id="eb284-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="eb284-115">Bkz: **tooadd hello Twilio kitaplıkları tooyour web rolü projesi**, bu konunun devamındaki.</span><span class="sxs-lookup"><span data-stu-id="eb284-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="eb284-116">Temel bir oluşturma konusunda bilgi sahibi olmanız gerekir [Azure Web rolü][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="eb284-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="eb284-117"><a name="howtocreateform"></a>Nasıl yapılır: arama yapmak için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb284-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="eb284-118"><a id="use_nuget"></a>tooadd hello Twilio kitaplıkları tooyour web rolü projesi:</span><span class="sxs-lookup"><span data-stu-id="eb284-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="eb284-119">Çözümünüzü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="eb284-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="eb284-120">Sağ **başvurular**.</span><span class="sxs-lookup"><span data-stu-id="eb284-120">Right-click **References**.</span></span>
3. <span data-ttu-id="eb284-121">Tıklatın **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="eb284-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="eb284-122">Tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="eb284-122">Click **Online**.</span></span>
5. <span data-ttu-id="eb284-123">Merhaba arama çevrimiçi kutusuna *twilio*.</span><span class="sxs-lookup"><span data-stu-id="eb284-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="eb284-124">Tıklatın **yükleme** hello Twilio paketinizdeki.</span><span class="sxs-lookup"><span data-stu-id="eb284-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="eb284-125">koddan hello nasıl toocreate web form arama yapmak için tooretrieve kullanıcı verileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="eb284-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="eb284-126">Bu örnekte, bir ASP.NET Web rolü adlı **TwilioCloud** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb284-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="eb284-127"><a id="howtocreatecode"></a>Nasıl yapılır: hello kod toomake hello çağrı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb284-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="eb284-128">Merhaba hello kullanıcı hello form tamamlandığında olarak adlandırılır, aşağıdaki kod, hello çağrı iletisi oluşturur ve hello çağrı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb284-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="eb284-129">Bu örnekte, hello kod hello onclick olay işleyicisini hello düğmesinin hello form üzerinde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="eb284-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="eb284-130">(Twilio hesabı ve kimlik doğrulama belirteci çok atanan hello yer tutucu değerlerini yerine kullanım`accountSID` ve `authToken` aşağıdaki hello kodda.)</span><span class="sxs-lookup"><span data-stu-id="eb284-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

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

<span data-ttu-id="eb284-131">Merhaba çağrı yapılır ve hello Twilio uç noktası, API sürümü ve hello arama durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="eb284-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="eb284-132">ekran görüntüsü gösterildiği çıkış çalıştırmak bir örnekten aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="eb284-132">hello following screenshot shows output from a sample run.</span></span>

![Twilio ve ASP.NET kullanılarak azure çağrı yanıtı][twilio_dotnet_basic_form_output]

<span data-ttu-id="eb284-134">TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="eb284-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="eb284-135">Hakkında daha fazla bilgi &lt;Say&gt; ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="eb284-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="eb284-136"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb284-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="eb284-137">Bu kod tooshow sağlanan Azure üzerinde ASP.NET web rolünde Twilio kullanarak, temel işlevleri.</span><span class="sxs-lookup"><span data-stu-id="eb284-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="eb284-138">TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb284-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="eb284-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="eb284-139">For example:</span></span>

* <span data-ttu-id="eb284-140">Bir web formu kullanmak yerine, Azure Blob Depolama veya bir Azure SQL veritabanı örneği toostore telefon numaralarını kullanın ve metin arama.</span><span class="sxs-lookup"><span data-stu-id="eb284-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="eb284-141">Azure BLOB'ları kullanma hakkında daha fazla bilgi için bkz: [nasıl toouse hello Azure Blob Depolama hizmetine .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="eb284-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="eb284-142">SQL veritabanı kullanma hakkında daha fazla bilgi için bkz: [nasıl toouse Azure SQL veritabanı .NET uygulamalarında][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="eb284-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="eb284-143">Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio hesap Kimliğini ve kimlik doğrulama belirteci hello değerlerde kodlamak formunuz yerine dağıtımınızın yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="eb284-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="eb284-144">Merhaba hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="eb284-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="eb284-145">Merhaba Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="eb284-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="eb284-146">Twilio hakkında daha fazla bilgi [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="eb284-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="eb284-147"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="eb284-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="eb284-148">Nasıl toouse Twilio azure'dan ses ve SMS özellikleri</span><span class="sxs-lookup"><span data-stu-id="eb284-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
