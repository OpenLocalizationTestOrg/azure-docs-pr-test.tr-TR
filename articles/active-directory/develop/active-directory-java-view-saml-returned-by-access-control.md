---
title: "Görünüm erişim denetimi hizmeti (Java) tarafından döndürülen SAML"
description: "Azure üzerinde barındırılan Java uygulamalarını erişim denetim Hizmeti'nde tarafından döndürülen SAML görüntülemeyi öğrenin."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: 1552e624a4703138ab82f7133ceaec3dbd04e1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="e389e-103">Azure erişim denetimi hizmeti tarafından döndürülen SAML görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e389e-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="e389e-104">Bu kılavuz temel güvenlik onaylama işlemi biçimlendirme dili (uygulamanızı Azure erişim denetimi Hizmeti'nden (ACS) tarafından döndürülen SAML) görüntülemek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e389e-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="e389e-105">Kılavuzu derlemeler [kimlik doğrulaması Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile nasıl](active-directory-java-authenticate-users-access-control-eclipse.md) SAML bilgilerini görüntüler kod sağlayarak konu.</span><span class="sxs-lookup"><span data-stu-id="e389e-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="e389e-106">Tamamlanan uygulama aşağıdakine benzer görünecektir.</span><span class="sxs-lookup"><span data-stu-id="e389e-106">The completed application will look similar to the following.</span></span>

![Örnek SAML çıktı][saml_output]

<span data-ttu-id="e389e-108">ACS hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next_steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e389e-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="e389e-109">Azure Erişim Hizmetleri Denetim filtresi topluluk teknoloji önizlemesidir.</span><span class="sxs-lookup"><span data-stu-id="e389e-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="e389e-110">Yayın öncesi yazılım olarak bunu resmi olarak Microsoft tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="e389e-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e389e-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e389e-111">Prerequisites</span></span>
<span data-ttu-id="e389e-112">Bu Kılavuzu'ndaki görevleri tamamlamak için örnek: tamamlamak [kimlik doğrulaması Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile nasıl](active-directory-java-authenticate-users-access-control-eclipse.md) ve Bu öğretici için başlangıç noktası olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="e389e-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="e389e-113">Derleme yolu ve dağıtım derlemesi için JspWriter kitaplığı Ekle</span><span class="sxs-lookup"><span data-stu-id="e389e-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="e389e-114">İçeren kitaplığı eklemek **javax.servlet.jsp.JspWriter** derleme yolu ve dağıtım derleme sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e389e-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="e389e-115">Tomcat kullanıyorsanız, kitaplığıdır **jsp api.jar**, Apache bulunan **lib** klasör.</span><span class="sxs-lookup"><span data-stu-id="e389e-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="e389e-116">Eclipse'nın Proje Gezgini'nde sağ **MyACSHelloWorld**, tıklatın **yapı yolu**,'ı tıklatın **oluşturma yolunu Yapılandır**,'ı tıklatın **kitaplıkları**sekmesini ve ardından **dış Jar'lar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e389e-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="e389e-117">İçinde **JAR seçimi** iletişim kutusunda, gerekli JAR gidin, onu seçin ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="e389e-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="e389e-118">İle **MyACSHelloWorld özelliklerini** iletişim hala açık tıklatın **dağıtım derleme**.</span><span class="sxs-lookup"><span data-stu-id="e389e-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="e389e-119">İçinde **Web dağıtımı derleme** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e389e-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="e389e-120">İçinde **yeni derleme yönergesi** iletişim kutusunda, tıklatın **Java derleme yolu girişleri** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e389e-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="e389e-121">Uygun kitaplığı seçin ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="e389e-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="e389e-122">Tıklatın **Tamam** kapatmak için **MyACSHelloWorld özelliklerini** iletişim.</span><span class="sxs-lookup"><span data-stu-id="e389e-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="e389e-123">SAML görüntülenecek JSP dosyası değiştirme</span><span class="sxs-lookup"><span data-stu-id="e389e-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="e389e-124">Değiştirme **index.jsp** aşağıdaki kodu kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="e389e-124">Modify **index.jsp** to use the following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate the child nodes of the doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-the-application"></a><span data-ttu-id="e389e-125">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e389e-125">Run the application</span></span>
1. <span data-ttu-id="e389e-126">Uygulamanızı bilgisayar öykünücüsünde çalıştırın veya adresinde belgelenen adımları kullanarak Azure dağıtmak [kimlik doğrulaması Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile nasıl](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="e389e-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="e389e-127">Bir tarayıcıyı başlatın ve web uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="e389e-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="e389e-128">Uygulamanıza oturum açtıktan sonra kimlik sağlayıcısı tarafından sağlanan güvenlik onaylama işlemi SAML bilgilerini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e389e-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e389e-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e389e-129">Next steps</span></span>
<span data-ttu-id="e389e-130">Biraz daha ACS'ın işlevselliği inceleyin ve daha karmaşık senaryolarıyla denemeler yapmak için bkz: [erişim denetimi hizmeti 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="e389e-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
