---
title: "Twilio (.NET) bir telefon araması yapma | Microsoft Docs"
description: "Bir telefon araması yapın ve Azure üzerinde Twilio API hizmetiyle SMS mesajı göndermek öğrenin. .NET ile yazılan kod örnekleri."
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
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="a4eda-104">Azure üzerinde bir web rolü Twilio kullanarak bir telefon araması yapma</span><span class="sxs-lookup"><span data-stu-id="a4eda-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="a4eda-105">Bu kılavuz Twilio Azure üzerinde barındırılan bir web sayfasından bir arama yapmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4eda-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="a4eda-106">Sonuçta elde edilen uygulama, aşağıdaki ekran görüntüsünde gösterildiği gibi verilen sayıda ve ileti ile arama yapmak için kullanıcıya sorar.</span><span class="sxs-lookup"><span data-stu-id="a4eda-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Twilio ve ASP.NET kullanarak azure çağrı formu][twilio_dotnet_basic_form]

## <span data-ttu-id="a4eda-108"><a name="twilio-prereqs"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a4eda-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="a4eda-109">Bu konudaki kodu kullanmak için aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4eda-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="a4eda-110">Twilio hesabı ve kimlik doğrulaması almak belirtecine [Twilio konsol][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="a4eda-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="a4eda-111">Twilio ile çalışmaya başlamak için oturum açın [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="a4eda-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="a4eda-112">Konumundaki fiyatlandırma değerlendirebilir [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="a4eda-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="a4eda-113">Twilio tarafından sağlanan API'si hakkında daha fazla bilgi için bkz: [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="a4eda-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="a4eda-114">Ekleme *Twilio .NET kitaplığı* web rolünüz.</span><span class="sxs-lookup"><span data-stu-id="a4eda-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="a4eda-115">Bkz: **Twilio kitaplıkları web rolü projenize eklemek için**, bu konunun devamındaki.</span><span class="sxs-lookup"><span data-stu-id="a4eda-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="a4eda-116">Temel bir oluşturma konusunda bilgi sahibi olmanız gerekir [Azure Web rolü][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="a4eda-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="a4eda-117"><a name="howtocreateform"></a>Nasıl yapılır: arama yapmak için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4eda-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="a4eda-118"><a id="use_nuget"></a>Twilio kitaplıkları web rolü projenize eklemek için:</span><span class="sxs-lookup"><span data-stu-id="a4eda-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="a4eda-119">Çözümünüzü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="a4eda-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="a4eda-120">Sağ **başvurular**.</span><span class="sxs-lookup"><span data-stu-id="a4eda-120">Right-click **References**.</span></span>
3. <span data-ttu-id="a4eda-121">Tıklatın **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="a4eda-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="a4eda-122">Tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="a4eda-122">Click **Online**.</span></span>
5. <span data-ttu-id="a4eda-123">Arama çevrimiçi kutuya yazın *twilio*.</span><span class="sxs-lookup"><span data-stu-id="a4eda-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="a4eda-124">Tıklatın **yükleme** Twilio paketinizdeki.</span><span class="sxs-lookup"><span data-stu-id="a4eda-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="a4eda-125">Aşağıdaki kod, arama yapmak için kullanıcı verilerini almak için web formu oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4eda-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="a4eda-126">Bu örnekte, bir ASP.NET Web rolü adlı **TwilioCloud** oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a4eda-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="a4eda-127"><a id="howtocreatecode"></a>Nasıl yapılır: arama yapmak için kod oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4eda-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="a4eda-128">Kullanıcı formu tamamlandığında olarak adlandırılır, aşağıdaki kod, arama iletisi oluşturur ve çağrı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a4eda-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="a4eda-129">Bu örnekte, formdaki düğmenin onclick olay işleyicisini kod çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="a4eda-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="a4eda-130">(Kullanım Twilio hesabı ve kimlik doğrulama belirteci atanan yer tutucu değerlerini yerine `accountSID` ve `authToken` aşağıdaki kodda.)</span><span class="sxs-lookup"><span data-stu-id="a4eda-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

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
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="a4eda-131">Çağrı yapılır ve Twilio uç noktası, API sürümü ve arama durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a4eda-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="a4eda-132">Aşağıdaki ekran görüntüsünde bir örnek çalışma çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4eda-132">The following screenshot shows output from a sample run.</span></span>

![Twilio ve ASP.NET kullanılarak azure çağrı yanıtı][twilio_dotnet_basic_form_output]

<span data-ttu-id="a4eda-134">TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="a4eda-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="a4eda-135">Hakkında daha fazla bilgi &lt;Say&gt; ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="a4eda-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="a4eda-136"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4eda-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a4eda-137">Bu kod, bir ASP.NET web rolünde Azure ile ilgili Twilio kullanarak temel işlevselliğini göstermek için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a4eda-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="a4eda-138">Azure'a üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4eda-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="a4eda-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a4eda-139">For example:</span></span>

* <span data-ttu-id="a4eda-140">Bir web formu kullanmak yerine, Azure Blob storage veya Azure SQL veritabanı örneği telefon numaralarını depolamak ve metin çağırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4eda-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="a4eda-141">Azure BLOB'ları kullanma hakkında daha fazla bilgi için bkz: [.NET ile Azure Blob Depolama hizmetini kullanmayı][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="a4eda-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="a4eda-142">SQL veritabanı kullanma hakkında daha fazla bilgi için bkz: [.NET uygulamalarında Azure SQL Database kullanmayı][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="a4eda-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="a4eda-143">Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` hesap Kimliğini ve kimlik doğrulama belirteci form değerleri sabit kodlama yerine dağıtımınızın yapılandırma ayarları Twilio alınamadı.</span><span class="sxs-lookup"><span data-stu-id="a4eda-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="a4eda-144">Hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="a4eda-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="a4eda-145">Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="a4eda-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="a4eda-146">Twilio hakkında daha fazla bilgi [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="a4eda-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="a4eda-147"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a4eda-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a4eda-148">Azure'dan ses ve SMS özelliklerine yönelik Twilio kullanma</span><span class="sxs-lookup"><span data-stu-id="a4eda-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
