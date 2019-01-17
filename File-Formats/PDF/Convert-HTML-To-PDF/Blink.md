---
title: Converting HTML to PDF | Syncfusion
description: Learn how to convert HTML to PDF using 3 different rendering engines (Blink, WebKit and IE) with various features like TOC, partial web page to PDF etc.
platform: file-formats
control: PDF
documentation: UG
---
# Conversion using Blink Rendering

Syncfusion Essential HTML converter supports HTML to PDF conversion by using the advanced Blink rendering engine. This converter can be easily integrated into any application on .NET platforms such as Windows Forms, WPF, ASP.NET, and ASP.NET MVC to convert URLs, HTML string, SVG and MHTML to PDF. 

## Prerequisites

<b>Minimum product version:</b> 16.3.0.21

<b>Minimum .NET Framework version:</b> 4.5 and above

* Latest version of Essential HTML converter can be downloaded from the below link,

    [https://www.syncfusion.com/downloads/latest-version](https://www.syncfusion.com/downloads/latest-version)

* To convert HTML to PDF using Blink rendering engine, add the following assemblies or NuGet packages as reference to the project.

<b>Assemblies</b>

* Syncfusion.Compression.Base.dll
* Syncfusion.Pdf.Base.dll
* Syncfusion.HtmlConverter.Base.dll
* Newtonsoft.Json package (v6.0.8 or above)
* BlinkBinaries

The BlinkBinaries folder is available in the HTML converter installed location <span style="color:gray;font-size:14px"><i>($SystemDrive\Program Files (x86)\Syncfusion\HTMLConverter\xx.x.x.xx\BlinkBinaries)</i></span>. The physical path of this folder should be set to the <i>BlinkPath</i> property of BlinkConverterSettings.

<b>NuGet</b>

<table>
<tr>
<thead>
<th><b>Platform(s)</b></th>
<th><b>NuGet Package</b></th>
</thead>
</tr>
<tr>
<td>
Windows Forms
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.Blink.WinForms.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Blink.WinForms/)'| markdownify }}
</td>
</tr>
<tr>
<td>
WPF
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.Blink.Wpf.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Blink.Wpf/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.Blink.AspNet.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Blink.AspNet/)'| markdownify }}
</td>
</tr>
<tr>
<td>
ASP.NET MVC
</td>
<td>
{{'[Syncfusion.HtmlToPdfConverter.Blink.AspNet.Mvc5.nupkg](https://www.nuget.org/packages/Syncfusion.HtmlToPdfConverter.Blink.AspNet.Mvc5/)'| markdownify }}
</td>
</tr>
</table>

N> The above mentioned NuGet packages are available in [nuget.org](https://www.nuget.org/)

* The BlinkBinaries folder is available in the package installed location. Set the path of the BlinkBinaries folder from package location to the <i>BlinkPath</i> property of BlinkConverterSettings.

## URL to PDF

To convert website URL or local HTML file to PDF using Blink rendering engine, refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com");

//Save and close the PDF document 
document.Save("Output.pdf");

document.Close(true);


{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document 
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## HTML String to PDF

Blink rendering engine provides support for converting HTML string to PDF. While converting HTML string to PDF, converter provides option to specify the base URL.

<b>baseURL:</b> Path of the resources (images, style sheets, scripts.,) used in the input HTML string.

For the below HTML string, the baseURL will be the path of the <font color="blue"><i>syncfusion_logo.gif</i></font> image.

For example, if the above image is in <i>“C:/Temp/ HTMLFiles/syncfusion_logo.gif”</i> location then the baseURL will be as below,

<b>baseURL:</b> C:/Temp/HTMLFiles/

To convert the HTML string to PDF, refer to the following code snippet. 

{% tabs %}

{% highlight c# %}

//Initialize HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//HTML string and Base URL 
string htmlText = "<html><body><img src=\"syncfusion_logo.gif\" alt=\"Syncfusion_logo\" width=\"200\" height=\"70\"><p> Hello World</p></body></html>";

string baseUrl = @"C:/Temp/HTMLFiles/";

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert(htmlText, baseUrl);

//Save and close the PDF document 
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'HTML string and Base URL 
Dim htmlText As String = "<html><body><img src=""syncfusion_logo.gif"" alt=""Syncfusion_logo"" width=""200"" height=""70""><p> Hello World</p></body></html>"

Dim baseUrl As String = "C:/Temp/HTMLFiles/"

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert(htmlText, baseUrl)

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight html %}
<html>
<body>
<img src="syncfusion_logo.gif" alt="Syncfusion_logo" width="200" height="70">
<p> Hello World</p>
</body>
</html>

{% endhighlight %}

{% endtabs %}

## URL to Image

To convert website URL or local HTML file to Image using Blink rendering engine, refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to Image
Image[] image = htmlConverter.ConvertToImage("https://www.google.com");

//Save and dispose the image file
image[0].Save("Output.jpg");
image[0].Dispose();

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to Image
Dim image As Image[] = htmlConverter.ConvertToImage("https://www.google.com")

'Save and dispose the image file
image[0].Save("Output.jpg")

image[0].Dispose(True)

{% endhighlight %}

{% endtabs %}

## HTML String to Image

The Blink rendering engine supports converting HTML string to Image. While converting HTML string to Image, converter provides an option to specify the base URL.

<b>baseURL:</b> Path of the resources (images, style sheets, scripts.,) used in the input HTML string.

For the following HTML string, the baseURL will be the path of the <font color="blue"><i>syncfusion_logo.gif</i></font> image.

For example, if the previous image is in <i>“C:/Temp/ HTMLFiles/syncfusion_logo.gif”</i> location then the baseURL will be as follows.

<b>baseURL:</b> C:/Temp/HTMLFiles/

To convert the HTML string to Image, refer to the following code snippet.

{% tabs %} 

{% highlight c# %}

//Initialize HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//HTML string and Base URL
string htmlText = "<html><body><img src=\"syncfusion_logo.gif\" alt=\"Syncfusion_logo\" width=\"200\" height=\"70\"><p> Hello World</p></body></html>";

string baseUrl = @"C:/Temp/HTMLFiles/";

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to Image
Image[] image = htmlConverter.ConvertToImage(htmlText, baseUrl);

//Save and dispose the image file
image[0].Save("Output.jpg");
image[0].Dispose();

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'HTML string and Base URL
Dim htmlText As String = "<html><body><img src=""syncfusion_logo.gif"" alt=""Syncfusion_logo"" width=""200"" height=""70""><p> Hello World</p></body></html>"

Dim baseUrl As String = "C:/Temp/HTMLFiles/"

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to Image
Dim image As Image[] = htmlConverter.Convert(htmlText, baseUrl)

'Save and dispose the image file
image[0].Save("Output.jpg")
image[0].Dispose(True)

{% endhighlight %}

{% highlight html %}

<html>
<body>
    <img src="syncfusion_logo.gif" alt="Syncfusion_logo" width="200" height="70">
    <p> Hello World</p>
</body>
</html>

{% endhighlight %}

{% endtabs %}

## JavaScript

The Blink HTML converter supports enabling or disabling the JavaScript while converting HTML to PDF. Refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Disable JavaScript; By default, true
blinkConverterSettings.EnableJavaScript = false;

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Disable JavaScript; By default True
blinkConverterSettings.EnableJavaScript = False

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Additional delay

The Blink HTML converter provides option to set the AdditionalDelay property, while converting HTML to PDF. Additional delay is the waiting time of the converter for loading the external resources (styles, scripts, images and more). Refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

// Set additional delay; units in milliseconds
blinkConverterSettings.AdditionalDelay = 3000;

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{%  highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Set additional delay; units in milliseconds
blinkConverterSettings.AdditionalDelay = 3000

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Hyperlinks

The Blink HTML converter support preserving URL links from HTML to PDF. Refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Enable hyperlinks; By default - true
blinkConverterSettings.EnableHyperLink = false;

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = NewHtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Enable hyperlinks; By default - True
blinkConverterSettings.EnableHyperLink = False

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Media Type

The Blink HTML Converter allows selection of media type while converting HTML to PDF. Blink rendering engine supports <b>Screen</b> and <b>Print</b> media types. Refer to the following code snippet to select Print MediaType.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Set print media type
blinkConverterSettings.MediaType = MediaType.Print;

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"
'Set print media type
blinkConverterSettings.MediaType = MediaType.Print

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}


## Windows authentication

To convert the Windows authenticated webpage to the PDF document by providing the username and password. Refer the following code snippet.

{% tabs %}

{% highlight c# %}

// Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

blinkConverterSettings.Username = "username";

blinkConverterSettings.Password = "password";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.example.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

blinkConverterSettings.Username = "username"

blinkConverterSettings.Password = "password"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.example.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Form authentication

The Blink HTML converter provides support for form authentication by using cookies. The cookies are send to web server for form authentication when the HTML page is requested. Each cookie is represented by a name and value. Refer to the following code snippet.

{% tabs %}

{% highlight c# %}

// Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

// Add cookies as name and value pair

blinkConverterSettings.Cookies.Add("CookieName1", " CookieValue1");

blinkConverterSettings.Cookies.Add("CookieName2", " CookieValue2");


//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.example.com");

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Add cookies

blinkConverterSettings.Cookies.Add("Name1", "Value1")

blinkConverterSettings.Cookies.Add("Name2", "Value2")

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.example.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}


## Offline conversion

Blink HTML converter supports converting HTML to PDF in offline mode. While converting HTML to PDF in offline mode, the converter does not access the resources from the Internet. This may increase the performance in slow Internet connection.

N> If an online URL is converted in offline mode, the converter will generate empty PDF as it will not try to load any resource from online.

Refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Enable offline mode
blinkConverterSettings.EnableOfflineMode = true;

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Enable offline mode
blinkConverterSettings.EnableOfflineMode = True

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}

## Viewport

Adjusting HTML content size in PDF is possible by using the <i>ViewPortSize</i> property of Blink HTML converter. 
Refer to the following code snippet to adjust Blink viewport.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Set Blink viewport size
blinkConverterSettings.ViewPortSize = new Size(800, 0);

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("https://www.google.com")

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Set Blink viewport size
blinkConverterSettings.ViewPortSize = New Size(800, 0)

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}


## Windows status

Windows status can be used instead of additional delay. In additional delay, the amount of time required for loading the resources is unpredictable. This behavior can be avoided by using windows status.

N> This feature requires changes in the HTML file.

If windows status does not match in code and HTML, then the converter will meet with deadlock.
Refer to the following code snippet,

{% tabs %}

{% highlight c# %}

// Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

// Set windows status.
blinkConverterSettings.WindowStatus = "completed";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
PdfDocument document = htmlConverter.Convert("input.html");

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Set windows status.
blinkConverterSettings.WindowStatus = "completed"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("input.html")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% highlight html %}

<html>
<head>
</head>
<body>
    <div id="message">
        Wait for 2 Seconds
    </div>
    <script type="text/javascript">
        setTimeout(function () {
            document.getElementById("message").innerHTML = "Hello World!!";
            window.status = "completed";
        }, 2000);
    </script>
</body>
</html>

{% endhighlight %}

{% endtabs %}


## Temporary path

The Blink HTML converter launching chrome browser to perform conversion. While launching chrome browser, temporary files are created in a temporary folder. 
<br/>
By default, HTML converter takes system temporary path (C:\Users<<username»\AppData\Local\Temp or C:\Windows\Temp) to perform the conversion. 
<br/>
The temporary path can be changed by using the TempPath property of BlinkConverterSettings. If this property  is set, the converter uses the provided path to perform the conversion. Refer to the following code snippet.

{% tabs %}

{% highlight c# %}

//Initialize the HTML to PDF converter with Blink rendering engine
HtmlToPdfConverter htmlConverter = new HtmlToPdfConverter(HtmlRenderingEngine.Blink);

BlinkConverterSettings blinkConverterSettings = new BlinkConverterSettings();

//Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = @"/BlinkBinaries/";

//Set Temporary Path to generate temporary files
blinkConverterSettings.TempPath = @"C:/HtmlConversion/Temp/";

//Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings;

//Convert URL to PDF
htmlConverter.Convert("https://www.google.com");

//Save and close the PDF document
document.Save("Output.pdf");

document.Close(true);

{% endhighlight %}

{% highlight vb.net %}

'Initialize the HTML to PDF converter with Blink rendering engine
Dim htmlConverter As HtmlToPdfConverter = New HtmlToPdfConverter(HtmlRenderingEngine.Blink)

Dim blinkConverterSettings As BlinkConverterSettings = New BlinkConverterSettings()

'Set the BlinkBinaries folder path
blinkConverterSettings.BlinkPath = "/BlinkBinaries/"

'Set Temporary Path to generate temporary files
blinkConverterSettings.TempPath = "C:/HtmlConversion/Temp/"

'Assign Blink converter settings to HTML converter
htmlConverter.ConverterSettings = blinkConverterSettings

'Convert URL to PDF
Dim document As PdfDocument = htmlConverter.Convert("https://www.google.com")

'Save and close the PDF document
document.Save("Output.pdf")

document.Close(True)

{% endhighlight %}

{% endtabs %}