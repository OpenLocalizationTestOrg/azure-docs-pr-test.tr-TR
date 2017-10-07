---
title: "aaaView SAML döndürülen hello erişim denetimi hizmeti (Java) tarafından"
description: "Nasıl tooview SAML Java uygulamalarını hello erişim denetimi hizmeti tarafından döndürülen Azure üzerinde barındırılan öğrenin."
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
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Nasıl tooview SAML hello Azure erişim denetimi hizmeti tarafından döndürülen
Bu kılavuz size nasıl güvenlik onaylama işlemi biçimlendirme dili (SAML) temel tooview hello tooyour hello Azure erişim denetimi Hizmeti'nden (ACS) tarafından döndürülen gösterir. Merhaba Kılavuzu derlemeler üzerinde hello [nasıl tooAuthenticate Azure erişim denetimi hizmeti kullanılarak Eclipse Web kullanıcılarla](active-directory-java-authenticate-users-access-control-eclipse.md) hello SAML bilgilerini görüntüler kod sağlayarak konu. Tamamlanan Merhaba uygulaması benzer toohello aşağıdaki arar.

![Örnek SAML çıktı][saml_output]

Merhaba ACS hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next_steps) bölümü.

> [!NOTE]
> Hello Azure Erişim Hizmetleri Denetim filtresi topluluk teknoloji önizlemesidir. Yayın öncesi yazılım olarak bunu resmi olarak Microsoft tarafından desteklenmiyor.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
toocomplete hello görevler bu kılavuzda, tam örnek: Merhaba [nasıl tooAuthenticate Azure erişim denetimi hizmeti kullanılarak Eclipse Web kullanıcılarla](active-directory-java-authenticate-users-access-control-eclipse.md) ve hello Bu öğretici için başlangıç noktası olarak kullanın.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Yol ve dağıtım Hello JspWriter kitaplığı tooyour yapı derleme ekleyin
Merhaba içeren hello Kitaplığı eklemek **javax.servlet.jsp.JspWriter** sınıfı tooyour derleme yolu ve dağıtım derleme. Tomcat kullanıyorsanız, hello kitaplığıdır **jsp api.jar**, hello Apache bulunan **lib** klasör.

1. Eclipse'nın Proje Gezgini'nde sağ **MyACSHelloWorld**,'ı tıklatın **yapı yolu**,'ı tıklatın **oluşturma yolunu Yapılandır**, hello tıklatın **kitaplıkları** sekmesini ve ardından **dış Jar'lar Ekle**.
2. Merhaba, **JAR seçimi** iletişim kutusunda, toohello gidin gerekli JAR seçin ve ardından **açık**.
3. Merhaba ile **MyACSHelloWorld özelliklerini** iletişim hala açık tıklatın **dağıtım derleme**.
4. Merhaba, **Web dağıtımı derleme** iletişim kutusunda, tıklatın **Ekle**.
5. Merhaba, **yeni derleme yönergesi** iletişim kutusunda, tıklatın **Java derleme yolu girişleri** ve ardından **sonraki**.
6. Merhaba uygun kitaplığı seçin ve tıklatın **son**.
7. Tıklatın **Tamam** tooclose hello **MyACSHelloWorld özelliklerini** iletişim.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Merhaba JSP dosyası toodisplay SAML değiştirme
Değiştirme **index.jsp** toouse hello koddan.

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

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
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

            // Iterate hello child nodes of hello doc.
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

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
1. Uygulamanızı hello bilgisayar öykünücüsünde çalıştırın veya adresinde belgelenen hello adımları kullanarak tooAzure dağıtmak [nasıl tooAuthenticate Azure erişim denetimi hizmeti kullanılarak Eclipse Web kullanıcılarla](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Bir tarayıcıyı başlatın ve web uygulamasını açın. Tooyour uygulama açtıktan sonra hello güvenlik onaylama işlemi hello kimlik sağlayıcısı tarafından sağlanan SAML bilgilerini görürsünüz.

## <a name="next-steps"></a>Sonraki adımlar
toofurther ACS'ın işlevselliği ve daha karmaşık senaryolar ile tooexperiment keşfetmek için bkz: [erişim denetimi hizmeti 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
