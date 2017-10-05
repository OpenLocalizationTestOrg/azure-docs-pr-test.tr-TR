---
title: "Twilio (Java) telefon görüşmesi yapma | Microsoft Docs"
description: "Azure üzerinde bir Java uygulamasında Twilio kullanarak bir web sayfasından telefon görüşmesi öğrenin."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04ecb80a2a9e15b549b47138caf71c7e64bda500
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="721d9-103">Azure üzerinde bir Java uygulamasında Twilio kullanarak bir telefon araması yapma</span><span class="sxs-lookup"><span data-stu-id="721d9-103">How to Make a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="721d9-104">Aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından arama yapmak için Twilio nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="721d9-104">The following example shows you how you can use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="721d9-105">Sonuçta elde edilen uygulama telefon araması değerleri için aşağıdaki ekran görüntüsünde gösterildiği gibi ister.</span><span class="sxs-lookup"><span data-stu-id="721d9-105">The resulting application will prompt the user for phone call values, as shown in the following screen shot.</span></span>

![Twilio ve Java kullanarak azure çağrı formu][twilio_java]

<span data-ttu-id="721d9-107">Bu konudaki kodu kullanmak için aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="721d9-107">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="721d9-108">Twilio hesabı ve kimlik doğrulama alma belirteci.</span><span class="sxs-lookup"><span data-stu-id="721d9-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="721d9-109">Twilio ile çalışmaya başlamak için fiyatlandırma değerlendirmek [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="721d9-109">To get started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="721d9-110">Konumundaki kaydolabilirsiniz [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="721d9-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="721d9-111">Twilio tarafından sağlanan API'si hakkında daha fazla bilgi için bkz: [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="721d9-111">For information about the API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="721d9-112">Twilio JAR edinin.</span><span class="sxs-lookup"><span data-stu-id="721d9-112">Obtain the Twilio JAR.</span></span> <span data-ttu-id="721d9-113">Konumundaki [https://github.com/twilio/twilio-java][twilio_java_github], GitHub kaynakları indirmek ve kendi JAR oluşturabilir veya önceden oluşturulmuş bir JAR (veya ile bağımlılıklar olmadan) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721d9-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="721d9-114">Bu konu kodda, önceden oluşturulmuş bağımlılıkları ile TwilioJava 3.3.8 JAR kullanılarak yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="721d9-114">The code in this topic was written using the pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="721d9-115">JAR, Java derleme yolu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="721d9-115">Add the JAR to your Java build path.</span></span>
4. <span data-ttu-id="721d9-116">Bu Java uygulaması oluşturmak için Eclipse kullanıyorsanız, Twilio JAR Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerir.</span><span class="sxs-lookup"><span data-stu-id="721d9-116">If you are using Eclipse to create this Java application, include the Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="721d9-117">Bu Java uygulaması oluşturmak için Eclipse kullanmıyorsanız Twilio JAR Java uygulamanız aynı Azure rolünü içerdiği ve uygulamanızı sınıfı yoluna eklenen emin olun.</span><span class="sxs-lookup"><span data-stu-id="721d9-117">If you are not using Eclipse to create this Java application, ensure the Twilio JAR is included within the same Azure role as your Java application, and added to the class path of your application.</span></span>
5. <span data-ttu-id="721d9-118">Cacerts anahtar deposu MD5 parmak izi 67:CB:9 D ile Equifax güvenli sertifika yetkilisi sertifikasına sahip olmasını: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (seri numarasını 35:DE:F4:CF ve SHA1 parmak izi D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="721d9-118">Ensure your cacerts keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="721d9-119">Sertifika yetkilisi (CA) sertifikası budur [https://api.twilio.com] [ twilio_api_service] Twilio API'leri kullandığınızda çağrılan hizmet.</span><span class="sxs-lookup"><span data-stu-id="721d9-119">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="721d9-120">Bu CA sertifikası JDK'ın cacert depoya ekleme hakkında daha fazla bilgi için bkz: [Java CA sertifika deposu için bir sertifika ekleme][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="721d9-120">For information about adding this CA certificate to your JDK's cacert store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="721d9-121">Ayrıca, bilgileri aşina [Hello World uygulama kullanarak bir Azure araç setini Eclipse için oluşturma][azure_java_eclipse_hello_world], veya kullanıyorsanız azure'da Java uygulamaları barındırmak için başka teknikler ile Eclipse kullanmayan, kesinlikle önerilir.</span><span class="sxs-lookup"><span data-stu-id="721d9-121">Additionally, familiarity with the information at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="721d9-122">Arama yapmak için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="721d9-122">Create a web form for making a call</span></span>
<span data-ttu-id="721d9-123">Aşağıdaki kod, arama yapmak için kullanıcı verilerini almak için web formu oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="721d9-123">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="721d9-124">Bu örnekte, yeni bir dinamik web projesi adlı **TwilioCloud**, oluşturulduğu ve **callform.jsp** bir JSP dosyası olarak eklendi.</span><span class="sxs-lookup"><span data-stu-id="721d9-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is the call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-the-code-to-make-the-call"></a><span data-ttu-id="721d9-125">Çağrı yapmak için kod oluşturma</span><span class="sxs-lookup"><span data-stu-id="721d9-125">Create the code to make the call</span></span>
<span data-ttu-id="721d9-126">Kullanıcı tarafından callform.jsp görüntülenen form tamamlandığında olarak adlandırılır, aşağıdaki kod, arama iletisi oluşturur ve çağrı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="721d9-126">The following code, which is called when the user completes the form displayed by callform.jsp, creates the call message and generates the call.</span></span> <span data-ttu-id="721d9-127">Bu örneğin amaçları doğrultusunda JSP dosyası adlı **makecall.jsp** ve eklendi **TwilioCloud** projesi.</span><span class="sxs-lookup"><span data-stu-id="721d9-127">For purposes of this example, the JSP file is named **makecall.jsp** and was added to the **TwilioCloud** project.</span></span> <span data-ttu-id="721d9-128">(Kullanım Twilio hesabı ve kimlik doğrulama belirteci atanan yer tutucu değerlerini yerine **accountSID** ve **authToken** aşağıdaki kodda.)</span><span class="sxs-lookup"><span data-stu-id="721d9-128">(Use your Twilio account and authentication token instead of the placeholder values assigned to **accountSID** and **authToken** in the code below.)</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of the placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of the Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve the account, used later to retrieve the CallFactory.
         Account account = client.getAccount();

         // Display the client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display the API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve the values entered by the user.
         String callTo = request.getParameter("callTo");  
         // The Outgoing Caller ID, used for the From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in the user's text with '%20', 
         // to make the text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using the Twilio message and the user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display the message URL.
         out.println("<p>");
         out.println("The URL is " + Url);
         out.println("</p>");

         // Place the call From, To and URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

<span data-ttu-id="721d9-129">Çağrıyı yapan yanı sıra makecall.jsp Twilio uç noktası, API sürümü ve çağrı durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="721d9-129">In addition to making the call, makecall.jsp displays the Twilio endpoint, API version, and the call status.</span></span> <span data-ttu-id="721d9-130">Aşağıdaki ekran örneğidir:</span><span class="sxs-lookup"><span data-stu-id="721d9-130">An example is the following screen shot:</span></span>

![Twilio ve Java kullanarak azure çağrı yanıtı][twilio_java_response]

## <a name="run-the-application"></a><span data-ttu-id="721d9-132">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="721d9-132">Run the application</span></span>
<span data-ttu-id="721d9-133">Uygulamanızı çalıştırmak için üst düzey adımları şunlardır; Bu adımları bulunabilir ayrıntıları [Hello World uygulama kullanarak bir Azure araç setini Eclipse için oluşturma][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="721d9-133">Following are the high-level steps to run your application; details for these steps can be found at [Creating a Hello World Application Using the Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="721d9-134">Azure'a TwilioCloud WAR dışarı **approot** klasör.</span><span class="sxs-lookup"><span data-stu-id="721d9-134">Export your TwilioCloud WAR to the Azure **approot** folder.</span></span> 
2. <span data-ttu-id="721d9-135">Değiştirme **startup.cmd** TwilioCloud WAR sıkıştırmasını açmak için.</span><span class="sxs-lookup"><span data-stu-id="721d9-135">Modify **startup.cmd** to unzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="721d9-136">İşlem öykünücüsü için uygulamanızı derleyin.</span><span class="sxs-lookup"><span data-stu-id="721d9-136">Compile your application for the compute emulator.</span></span>
4. <span data-ttu-id="721d9-137">Dağıtımınızı işlem öykünücüsünde başlatın.</span><span class="sxs-lookup"><span data-stu-id="721d9-137">Start your deployment in the compute emulator.</span></span>
5. <span data-ttu-id="721d9-138">Bir tarayıcı açın ve Çalıştır **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="721d9-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="721d9-139">Değerleri girin, tıklatın **bu çağırmaya**ve ardından makecall.jsp sonuçlarında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721d9-139">Enter values in the form, click **Make this call**, and then see the results in makecall.jsp.</span></span>

<span data-ttu-id="721d9-140">Azure, bulut dağıtımını yeniden derleyebilirsiniz dağıtmaya hazır olduğunuzda, Azure'a dağıtma ve http:// çalıştırma*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp tarayıcıda (ve değer için alternatif  *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="721d9-140">When you are ready to deploy to Azure, recompile for deployment to the cloud, deploy to Azure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in the browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="721d9-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="721d9-141">Next steps</span></span>
<span data-ttu-id="721d9-142">Bu kod, Azure üzerinde Twilio Java kullanarak temel işlevselliğini göstermek için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="721d9-142">This code was provided to show you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="721d9-143">Azure'a üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721d9-143">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="721d9-144">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="721d9-144">For example:</span></span>

* <span data-ttu-id="721d9-145">Bir web formu kullanmak yerine, Azure storage bloblarında veya SQL veritabanı telefon numaralarını depolamak ve metin çağırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="721d9-145">Instead of using a web form, you could use Azure storage blobs or SQL Database to store phone numbers and call text.</span></span> <span data-ttu-id="721d9-146">Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [Java'dan Blob Depolama hizmetini kullanmayı][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="721d9-146">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="721d9-147">SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="721d9-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="721d9-148">Kullanabileceğinizi **RoleEnvironment.getConfigurationSettings** hesap Kimliğini ve kimlik doğrulama belirteci makecall.jsp değerleri sabit kodlama yerine dağıtımınızın yapılandırma ayarları Twilio alınamadı.</span><span class="sxs-lookup"><span data-stu-id="721d9-148">You could use **RoleEnvironment.getConfigurationSettings** to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in makecall.jsp.</span></span> <span data-ttu-id="721d9-149">Hakkında bilgi için **RoleEnvironment** sınıfı için bkz: [jsp biçiminde Azure hizmeti çalışma zamanı kitaplığını kullanarak] [ azure_runtime_jsp] ve Azurehizmetiçalışmazamanıpaketibelgeleri[http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="721d9-149">For information about the **RoleEnvironment** class, see [Using the Azure Service Runtime Library in JSP][azure_runtime_jsp] and the Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="721d9-150">Twilio tarafından sağlanan URL makecall.jsp kodunu atar [http://twimlets.com/message][twimlet_message_url], **Url** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="721d9-150">The makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], to the **Url** variable.</span></span> <span data-ttu-id="721d9-151">Bu URL çağrısı ile devam etmek nasıl Twilio bildiren bir Twilio biçimlendirme dili (TwiML) yanıt sağlar.</span><span class="sxs-lookup"><span data-stu-id="721d9-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how to proceed with the call.</span></span> <span data-ttu-id="721d9-152">Örneğin, döndürülen TwiML içerebilir bir  **&lt;Say&gt;**  çağrısı alıcıya konuşulan metin sonuçlanır fiil.</span><span class="sxs-lookup"><span data-stu-id="721d9-152">For example, the TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken to the call recipient.</span></span> <span data-ttu-id="721d9-153">Twilio tarafından sağlanan URL kullanmak yerine, kendi hizmet Twilio'nın isteğine yanıt vermek için derleme; Daha fazla bilgi için bkz: [ses ve Java SMS yetenekler için kullanım Twilio nasıl][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="721d9-153">Instead of using the Twilio-provided URL, you could build your own service to respond to Twilio's request; for more information, see [How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="721d9-154">TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml]ve hakkında daha fazla bilgi  **&lt;Say&gt;**  ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="721d9-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="721d9-155">Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="721d9-155">Read the Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="721d9-156">Twilio hakkında ek bilgi için bkz: [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="721d9-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="721d9-157">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="721d9-157">See Also</span></span>
* <span data-ttu-id="721d9-158">[Ses ve Java SMS yetenekler için Twilio kullanma][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="721d9-158">[How to Use Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="721d9-159">[Bir sertifika Java CA sertifika depolama alanına ekleme][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="721d9-159">[Adding a Certificate to the Java CA Certificate Store][add_ca_cert]</span></span>

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
