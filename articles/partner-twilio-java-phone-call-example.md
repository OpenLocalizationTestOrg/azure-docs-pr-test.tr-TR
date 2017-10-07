---
title: "aaaHow tooMake Twilio (Java) bir telefon çağrısında | Microsoft Docs"
description: "Nasıl toomake bir telefon çağrısı Azure üzerinde bir Java uygulamasında Twilio kullanarak bir web sayfasından öğrenin."
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
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir Java uygulamasında
Merhaba aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından bir çağrı Twilio toomake nasıl kullanabileceğinizi gösterir. Merhaba sonuç uygulaması hello aşağıdaki ekran görüntüsü gösterildiği gibi hello kullanıcıdan telefon araması değerlerini ister.

![Twilio ve Java kullanarak azure çağrı formu][twilio_java]

Toodo hello aşağıdakilere ihtiyacınız olacak toouse hello kod bu konuda:

1. Twilio hesabı ve kimlik doğrulama alma belirteci. tooget Twilio ile kullanmaya değerlendirmek, fiyatlandırma [http://www.twilio.com/pricing][twilio_pricing]. Konumundaki kaydolabilirsiniz [https://www.twilio.com/try-twilio][try_twilio]. Merhaba Twilio tarafından sağlanan API hakkında daha fazla bilgi için bkz: [http://www.twilio.com/api][twilio_api].
2. Merhaba Twilio JAR edinin. Konumundaki [https://github.com/twilio/twilio-java][twilio_java_github], hello GitHub kaynakları indirmek ve kendi JAR oluşturabilir veya önceden oluşturulmuş bir JAR (veya ile bağımlılıklar olmadan) yükleyebilirsiniz.
   Bu konudaki Hello kod bağımlılıkları ile TwilioJava 3.3.8 JAR önceden oluşturulmuş hello kullanılarak yazılmıştır.
3. Java derleme yolu hello JAR tooyour ekleyin.
4. Bu Java uygulaması Eclipse toocreate kullanıyorsanız, hello Twilio JAR Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerir. Bu Java uygulaması Eclipse toocreate kullanmıyorsanız hello Twilio JAR hello içinde dahil olduğundan emin olun, Java uygulama ve eklenen toohello sınıf yolu uygulamanızın olarak aynı Azure rol.
5. Cacerts anahtar deposu MD5 parmak izi 67:CB:9 D ile Merhaba Equifax güvenli sertifika yetkilisi sertifikasına sahip olmasını: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Merhaba numarası 35:DE:F4:CF ve hello SHA1 parmak izi D2:32:09:AD:23:D seri 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Merhaba sertifika yetkilisi (CA) sertifikası hello için budur [https://api.twilio.com] [ twilio_api_service] Twilio API'leri kullandığınızda çağrılan hizmet. Bu CA sertifikası tooyour JDK'ın cacert depolama ekleme hakkında daha fazla bilgi için bkz: [sertifika toohello Java CA sertifika deposuna ekleme][add_ca_cert].

Merhaba bilgilerine ek olarak, bir aşina [bir Hello World uygulamasını kullanarak hello Eclipse için Azure araç seti oluşturma][azure_java_eclipse_hello_world], ya da Azure IF içinde Java uygulamalarını barındırmak için başka teknikler, Eclipse kullanmıyorsanız, kesinlikle önerilir.

## <a name="create-a-web-form-for-making-a-call"></a>Arama yapmak için web formu oluşturma
koddan hello nasıl toocreate web form arama yapmak için tooretrieve kullanıcı verileri gösterir. Bu örnekte, yeni bir dinamik web projesi adlı **TwilioCloud**, oluşturulduğu ve **callform.jsp** bir JSP dosyası olarak eklendi.

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
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
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

## <a name="create-hello-code-toomake-hello-call"></a>Merhaba kod toomake hello çağrı oluşturma
Merhaba hello kullanıcı callform.jsp tarafından görüntülenen hello formun tamamlandığında olarak adlandırılır, aşağıdaki kod, hello çağrı iletisi oluşturur ve hello çağrı oluşturur. Bu örneğin amaçları doğrultusunda hello JSP dosyası adlı **makecall.jsp** ve toohello eklendi **TwilioCloud** projesi. (Twilio hesabı ve kimlik doğrulama belirteci çok atanan hello yer tutucu değerlerini yerine kullanım**accountSID** ve **authToken** aşağıdaki hello kodda.)

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
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
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

Ayrıca toomaking Merhaba çağrısı, makecall.jsp hello Twilio uç noktası, API sürümü ve hello çağrı durumunu görüntüler. Aşağıdaki ekran görüntüsü hello buna bir örnektir:

![Twilio ve Java kullanarak azure çağrı yanıtı][twilio_java_response]

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
Aşağıdaki olan hello üst düzey adımları toorun uygulamanızı; Bu adımları bulunabilir ayrıntıları [bir Hello World uygulamasını kullanarak hello Eclipse için Azure araç seti oluşturma][azure_java_eclipse_hello_world].

1. TwilioCloud WAR toohello Azure verme **approot** klasör. 
2. Değiştirme **startup.cmd** toounzip TwilioCloud WAR.
3. Merhaba işlem öykünücüsü için uygulamanızı derleyin.
4. Dağıtımınızı hello işlem öykünücüsünde başlatın.
5. Bir tarayıcı açın ve Çalıştır **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Değerleri hello girin, tıklatın **bu çağrıyı yapmak**ve ardından makecall.jsp hello sonuçlarında görebilirsiniz.

Hazır toodeploy tooAzure olduğunda, dağıtım toohello bulut için yeniden derleyin, tooAzure dağıtmak ve http:// çalıştırmak*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp hello tarayıcıda ( içindeğeryerine*your_hosted_name*).

## <a name="next-steps"></a>Sonraki adımlar
Bu kod tooshow sağlanan Azure üzerinde Java Twilio kullanarak, temel işlevleri. TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz. Örneğin:

* Bir web formu kullanmak yerine, Azure storage bloblarında veya SQL veritabanı toostore telefon numaralarını kullanın ve metin arama. Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse hello Java'dan Blob Depolama hizmetinin][howto_blob_storage_java]. SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java][howto_sql_azure_java].
* Kullanabileceğinizi **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio hesap Kimliğini ve kimlik doğrulama belirteci makecall.jsp hello değerleri sabit kodlama yerine dağıtımınızın yapılandırma ayarları. Merhaba hakkında bilgi için **RoleEnvironment** sınıfı için bkz: [kullanma hello Azure hizmeti Çalışma Zamanı Kitaplığı'nda JSP] [ azure_runtime_jsp] ve hello Azure hizmeti çalışma zamanı paketi belgeleri [http://dl.windowsazure.com/javadoc][azure_javadoc].
* Merhaba makecall.jsp kodunu atar Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url], toohello **Url** değişkeni. Bu URL'yi nasıl tooproceed hello ile çağrı Twilio bildiren bir Twilio biçimlendirme dili (TwiML) yanıt sağlar. Örneğin, hello döndürülen TwiML içerebilir bir  **&lt;Say&gt;**  konuşulan toohello çağrı alıcı olan metinde sonuçları fiil. Merhaba Twilio tarafından sağlanan URL kullanmak yerine, kendi hizmet toorespond tooTwilio's isteği oluşturabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooUse ses ve Java SMS yetenekler için Twilio][howto_twilio_voice_sms_java]. TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml]ve hakkında daha fazla bilgi  **&lt;Say&gt;**  ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Merhaba Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].

Twilio hakkında ek bilgi için bkz: [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Ayrıca Bkz.
* [Nasıl tooUse Twilio ses ve Java SMS özellikleri][howto_twilio_voice_sms_java]
* [Sertifika toohello Java CA sertifika deposuna ekleme][add_ca_cert]

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
