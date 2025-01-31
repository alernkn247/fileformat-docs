---
title: Create, read, and edit Excel files in .NET MAUI | Syncfusion
description: Explains how to create, read, and edit Excel documents in .NET MAUI applications using Syncfusion Excel Library.
platform: maui
control: XlsIO
documentation: UG
---
# Create, read, and edit Excel files in .NET MAUI

Syncfusion Excel library for .NET MAUI platform can be used to create, read, edit Excel files. This also convert Excel files to PDF. Syncfusion Excel library is compatible with .NET MAUI Windows, iOS, and Android platforms only.

**Prerequisites:**

To use the MAUI project templates, install the Mobile development with .NET extension for Visual Studio. For more details, refer [here](https://docs.microsoft.com/en-us/dotnet/maui/get-started/installation).

## Create a simple Excel report

The below steps illustrates creating a simple Invoice formatted Excel document in .NET MAUI.

1.Create a new project in VS2022, select the .NET MAUI App (Preview) template, and click the **Next** button.

![Create .NET MAUI application in Visual Studio](MAUI_images/MAUI_images_img1.png)

2.Enter the project name and click **Create**.

![Name the project](MAUI_images/MAUI_images_img2.png)

3.Install the [Syncfusion.XlsIO.NET](https://www.nuget.org/packages/Syncfusion.XlsIO.NET/) NuGet package as reference to your .NET MAUI application from [NuGet.org](https://www.nuget.org).

![Add XlsIO reference to the project](MAUI_images/MAUI_images_img3.png)

4.Add a new button to the **MainWindow.xaml** as shown below.

{% tabs %}
{% highlight c# %}
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MAUISample.MainPage"
             BackgroundColor="{DynamicResource SecondaryColor}">
     <ScrollView>    
       <Button 
                Text="Create Excel"
                FontAttributes="Bold"
                Grid.Row="3"
                Clicked="createExcel_Click"
                HorizontalOptions="Center" 
                VerticalOptions="Center"/>
      </ScrollView>
</ContentPage>
{% endhighlight %}
{% endtabs %}

5.Include the following namespaces in the **MainWindow.xaml.cs** file.

{% tabs %}  
{% highlight c# %}
using Syncfusion.XlsIO;
using System.IO;
using System.Reflection;
{% endhighlight %}
{% endtabs %} 

6.Add a new action method **createExcel_Click** in MainWindow.xaml.cs and include the below code snippet to **create an Excel document**.

{% tabs %}  
{% highlight c# %}
//Create an instance of ExcelEngine.
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    //Create a workbook with a worksheet
    IWorkbook workbook = application.Workbooks.Create(1);

    //Access first worksheet from the workbook instance.
    IWorksheet worksheet = workbook.Worksheets[0];

    Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
    Stream inputStream = executingAssembly.GetManifestResourceStream("MAUISample.AdventureCycles-Logo.png");

    //Add a picture
    IPictureShape shape = worksheet.Pictures.AddPicture(1, 1, inputStream, 20, 20);

    //Disable gridlines in the worksheet
    worksheet.IsGridLinesVisible = false;

    //Enter values to the cells from A3 to A5
    worksheet.Range["A3"].Text = "46036 Michigan Ave";
    worksheet.Range["A4"].Text = "Canton, USA";
    worksheet.Range["A5"].Text = "Phone: +1 231-231-2310";

    //Make the text bold
    worksheet.Range["A3:A5"].CellStyle.Font.Bold = true;

    //Merge cells
    worksheet.Range["D1:E1"].Merge();

    //Enter text to the cell D1 and apply formatting.
    worksheet.Range["D1"].Text = "INVOICE";
    worksheet.Range["D1"].CellStyle.Font.Bold = true;
    worksheet.Range["D1"].CellStyle.Font.RGBColor = Syncfusion.Drawing.Color.FromArgb(0, 42, 118, 189);
    worksheet.Range["D1"].CellStyle.Font.Size = 35;

    //Apply alignment in the cell D1
    worksheet.Range["D1"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignRight;
    worksheet.Range["D1"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignTop;

    //Enter values to the cells from D5 to E8
    worksheet.Range["D5"].Text = "INVOICE#";
    worksheet.Range["E5"].Text = "DATE";
    worksheet.Range["D6"].Number = 1028;
    worksheet.Range["E6"].Value = "12/31/2018";
    worksheet.Range["D7"].Text = "CUSTOMER ID";
    worksheet.Range["E7"].Text = "TERMS";
    worksheet.Range["D8"].Number = 564;
    worksheet.Range["E8"].Text = "Due Upon Receipt";

    //Apply RGB backcolor to the cells from D5 to E8
    worksheet.Range["D5:E5"].CellStyle.Color = Syncfusion.Drawing.Color.FromArgb(0, 42, 118, 189);
    worksheet.Range["D7:E7"].CellStyle.Color = Syncfusion.Drawing.Color.FromArgb(0, 42, 118, 189);

    //Apply known colors to the text in cells D5 to E8
    worksheet.Range["D5:E5"].CellStyle.Font.Color = ExcelKnownColors.White;
    worksheet.Range["D7:E7"].CellStyle.Font.Color = ExcelKnownColors.White;

    //Make the text as bold from D5 to E8
    worksheet.Range["D5:E8"].CellStyle.Font.Bold = true;

    //Apply alignment to the cells from D5 to E8
    worksheet.Range["D5:E8"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;
    worksheet.Range["D5:E5"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter;
    worksheet.Range["D7:E7"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter;
    worksheet.Range["D6:E6"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignTop;

    //Enter value and applying formatting in the cell A7
    worksheet.Range["A7"].Text = "  BILL TO";
    worksheet.Range["A7"].CellStyle.Color = Syncfusion.Drawing.Color.FromArgb(0, 42, 118, 189);
    worksheet.Range["A7"].CellStyle.Font.Bold = true;
    worksheet.Range["A7"].CellStyle.Font.Color = ExcelKnownColors.White;

    //Apply alignment
    worksheet.Range["A7"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignLeft;
    worksheet.Range["A7"].CellStyle.VerticalAlignment = ExcelVAlign.VAlignCenter;

    //Enter values in the cells A8 to A12
    worksheet.Range["A8"].Text = "Steyn";
    worksheet.Range["A9"].Text = "Great Lakes Food Market";
    worksheet.Range["A10"].Text = "20 Whitehall Rd";
    worksheet.Range["A11"].Text = "North Muskegon,USA";
    worksheet.Range["A12"].Text = "+1 231-654-0000";

    //Create a Hyperlink for e-mail in the cell A13
    IHyperLink hyperlink = worksheet.HyperLinks.Add(worksheet.Range["A13"]);
    hyperlink.Type = ExcelHyperLinkType.Url;
    hyperlink.Address = "Steyn@greatlakes.com";
    hyperlink.ScreenTip = "Send Mail";

    //Enter details of products and prices
    worksheet.Range["A15"].Text = "  DESCRIPTION";
    worksheet.Range["C15"].Text = "QTY";
    worksheet.Range["D15"].Text = "UNIT PRICE";
    worksheet.Range["E15"].Text = "AMOUNT";
    worksheet.Range["A16"].Text = "Cabrales Cheese";
    worksheet.Range["A17"].Text = "Chocos";
    worksheet.Range["A18"].Text = "Pasta";
    worksheet.Range["A19"].Text = "Cereals";
    worksheet.Range["A20"].Text = "Ice Cream";
    worksheet.Range["C16"].Number = 3;
    worksheet.Range["C17"].Number = 2;
    worksheet.Range["C18"].Number = 1;
    worksheet.Range["C19"].Number = 4;
    worksheet.Range["C20"].Number = 3;
    worksheet.Range["D16"].Number = 21;
    worksheet.Range["D17"].Number = 54;
    worksheet.Range["D18"].Number = 10;
    worksheet.Range["D19"].Number = 20;
    worksheet.Range["D20"].Number = 30;
    worksheet.Range["D23"].Text = "Total";

    //Apply number format
    worksheet.Range["D16:E22"].NumberFormat = "$.00";
    worksheet.Range["E23"].NumberFormat = "$.00";

    //Merge column A and B from row 15 to 22
    worksheet.Range["A15:B15"].Merge();
    worksheet.Range["A16:B16"].Merge();
    worksheet.Range["A17:B17"].Merge();
    worksheet.Range["A18:B18"].Merge();
    worksheet.Range["A19:B19"].Merge();
    worksheet.Range["A20:B20"].Merge();
    worksheet.Range["A21:B21"].Merge();
    worksheet.Range["A22:B22"].Merge();

    //Apply incremental formula for column Amount by multiplying Qty and UnitPrice
    application.EnableIncrementalFormula = true;
    worksheet.Range["E16:E20"].Formula = "=C16*D16";

    //Formula for Sum the total
    worksheet.Range["E23"].Formula = "=SUM(E16:E22)";

    //Apply borders
    worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thin;
    worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thin;
    worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Grey_25_percent;
    worksheet.Range["A16:E22"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Grey_25_percent;
    worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].LineStyle = ExcelLineStyle.Thin;
    worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].LineStyle = ExcelLineStyle.Thin;
    worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeTop].Color = ExcelKnownColors.Black;
    worksheet.Range["A23:E23"].CellStyle.Borders[ExcelBordersIndex.EdgeBottom].Color = ExcelKnownColors.Black;

    //Apply font setting for cells with product details
    worksheet.Range["A3:E23"].CellStyle.Font.FontName = "Arial";
    worksheet.Range["A3:E23"].CellStyle.Font.Size = 10;
    worksheet.Range["A15:E15"].CellStyle.Font.Color = ExcelKnownColors.White;
    worksheet.Range["A15:E15"].CellStyle.Font.Bold = true;
    worksheet.Range["D23:E23"].CellStyle.Font.Bold = true;

    //Apply cell color
    worksheet.Range["A15:E15"].CellStyle.Color = Syncfusion.Drawing.Color.FromArgb(0, 42, 118, 189);

    //Apply alignment to cells with product details
    worksheet.Range["A15"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignLeft;
    worksheet.Range["C15:C22"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;
    worksheet.Range["D15:E15"].CellStyle.HorizontalAlignment = ExcelHAlign.HAlignCenter;

    //Apply row height and column width to look good
    worksheet.Range["A1"].ColumnWidth = 36;
    worksheet.Range["B1"].ColumnWidth = 11;
    worksheet.Range["C1"].ColumnWidth = 8;
    worksheet.Range["D1:E1"].ColumnWidth = 18;
    worksheet.Range["A1"].RowHeight = 47;
    worksheet.Range["A2"].RowHeight = 15;
    worksheet.Range["A3:A4"].RowHeight = 15;
    worksheet.Range["A5"].RowHeight = 18;
    worksheet.Range["A6"].RowHeight = 29;
    worksheet.Range["A7"].RowHeight = 18;
    worksheet.Range["A8"].RowHeight = 15;
    worksheet.Range["A9:A14"].RowHeight = 15;
    worksheet.Range["A15:A23"].RowHeight = 18;

    MemoryStream ms = new MemoryStream();
    workbook.SaveAs(ms);
    ms.Position = 0;
	
    //Saves the memory stream as a file.
    DependencyService.Get<ISave>().SaveAndView("Invoice.xlsx", "application/excel", ms);
}
{% endhighlight %}
{% endtabs %}  

## Save and View the Excel document in windows

Add the following **SaveWindows.cs** file to the **Project-> Platforms-> Windows** directory to save and view the Excel document in the windows machine.

{% tabs %}
{% highlight c# %}
using Microsoft.Maui.Controls;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Windows.Storage;
using Windows.Storage.Pickers;
using Windows.Storage.Streams;
using Windows.UI.Popups;

[assembly: Dependency(typeof(SaveWindows))]

class SaveWindows : ISave
{
    public async Task SaveAndView(string filename, string contentType, MemoryStream stream)
    {
        StorageFile stFile;
        string extension = Path.GetExtension(filename);
        //Gets process windows handle to open the dialog in application process. 
        IntPtr windowHandle = System.Diagnostics.Process.GetCurrentProcess().MainWindowHandle;
        if (!Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.Phone.UI.Input.HardwareButtons"))
        {
            //Create as file save picker to save a file. 
            FileSavePicker savePicker = new FileSavePicker();
            savePicker.DefaultFileExtension = ".xlsx";
            savePicker.SuggestedFileName = filename;
            //Saves the file as Excel file.
            savePicker.FileTypeChoices.Add("XLSX", new List<string>() { ".xlsx" });

            WinRT.Interop.InitializeWithWindow.Initialize(savePicker, windowHandle);
            stFile = await savePicker.PickSaveFileAsync();
        }
        else
        {
            StorageFolder local = ApplicationData.Current.LocalFolder;
            stFile = await local.CreateFileAsync(filename, CreationCollisionOption.ReplaceExisting);
        }
        if (stFile != null)
        {
            using (IRandomAccessStream zipStream = await stFile.OpenAsync(FileAccessMode.ReadWrite))
            {
                //Write s compressed data from memory to file.
                using (Stream outstream = zipStream.AsStreamForWrite())
                {
                    outstream.SetLength(0);
                    //Saves the stream as a file.
                    byte[] buffer = stream.ToArray();
                    outstream.Write(buffer, 0, buffer.Length);
                    outstream.Flush();
                }
            }
            //Create a message dialog box. 
            MessageDialog msgDialog = new MessageDialog("Do you want to view the Document?", "File created.");
            UICommand yesCmd = new UICommand("Yes");
            msgDialog.Commands.Add(yesCmd);
            UICommand noCmd = new UICommand("No");
            msgDialog.Commands.Add(noCmd);

            WinRT.Interop.InitializeWithWindow.Initialize(msgDialog, windowHandle);

            //Showing a dialog box. 
            IUICommand cmd = await msgDialog.ShowAsync();
            if (cmd.Label == yesCmd.Label)
            {
                //Launch the saved file. 
                await Windows.System.Launcher.LaunchFileAsync(stFile);
            }
        }
    }
}
{% endhighlight %}
{% endtabs %}

## Save and View the Excel document in Android

Add the following **SaveAndroid.cs** file to the **Project-> Platforms-> Android** directory folder to save and view the Excel document in the Android Device.

{% tabs %}
{% highlight c# %}

using System;
using System.IO;
using Android.Content;
using Java.IO;
using System.Threading.Tasks;
using Android;
using Android.Content.PM;
using Microsoft.Maui.Controls;
using AndroidX.Core.Content;
using Android.OS;
using Microsoft.Maui.Essentials;

[assembly: Dependency(typeof(SaveAndroid))]

class SaveAndroid : ISave
{
    //Method to save document as a file in Android and view the saved document
    public async Task SaveAndView(string fileName, String contentType, MemoryStream stream)
    {
        string exception = string.Empty;
        string root = null;

        if (Android.OS.Environment.IsExternalStorageEmulated)
        {
            root = Android.App.Application.Context.GetExternalFilesDir(Android.OS.Environment.DirectoryDownloads).AbsolutePath;
        }
        else
            root = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);

        Java.IO.File myDir = new Java.IO.File(root + "/Syncfusion");
        myDir.Mkdir();

        Java.IO.File file = new Java.IO.File(myDir, fileName);

        if (file.Exists())
        {
            file.Delete();
        }

        try
        {
            FileOutputStream outs = new FileOutputStream(file);
            outs.Write(stream.ToArray());

            outs.Flush();
            outs.Close();
        }
        catch (Exception e)
        {
            exception = e.ToString();
        }
        if (file.Exists())
        {

            if (Build.VERSION.SdkInt >= Android.OS.BuildVersionCodes.N)
            {
                var fileUri = AndroidX.Core.Content.FileProvider.GetUriForFile(Android.App.Application.Context, Android.App.Application.Context.PackageName + ".provider", file);
                var intent = new Intent(Intent.ActionView);
                intent.SetData(fileUri);
                intent.AddFlags(ActivityFlags.NewTask);
                intent.AddFlags(ActivityFlags.GrantReadUriPermission);
                Android.App.Application.Context.StartActivity(intent);
            }
            else
            {
                var fileUri = Android.Net.Uri.Parse(file.AbsolutePath);
                var intent = new Intent(Intent.ActionView);
                intent.SetDataAndType(fileUri, contentType);
                intent = Intent.CreateChooser(intent, "Open File");
                intent.AddFlags(ActivityFlags.NewTask);
                Android.App.Application.Context.StartActivity(intent);
            }
        }
    }
}
{% endhighlight %}
{% endtabs %}

## Save and View the Excel document in iOS

Add the following **SaveIOS.cs** file to the **Project-> Platforms-> iOS** directory to save the Excel document in the iOS Device.

{% tabs %}
{% highlight c# %}
using System;
using System.Threading.Tasks;
using System.IO;
using UIKit;
using QuickLook;
using Microsoft.Maui.Controls;

[assembly: Dependency(typeof(SaveIOS))]

class SaveIOS : ISave
{
    public async Task SaveAndView(string filename, string contentType, MemoryStream stream)
    {
        string exception = string.Empty;
        string path = Environment.GetFolderPath(Environment.SpecialFolder.Personal);
        string filePath = Path.Combine(path, filename);
        try
        {
            FileStream fileStream = File.Open(filePath, FileMode.Create);
            stream.Position = 0;
            stream.CopyTo(fileStream);
            fileStream.Flush();
            fileStream.Close();
        }
        catch (Exception e)
        {
            exception = e.ToString();
        }
        if (contentType == "application/html" || exception != string.Empty)
            return;

        UIViewController currentController = UIApplication.SharedApplication.KeyWindow.RootViewController;
        while (currentController.PresentedViewController != null)
            currentController = currentController.PresentedViewController;
        UIView currentView = currentController.View;

        QLPreviewController qlPreview = new QLPreviewController();
        QLPreviewItem item = new QLPreviewItemBundle(filename, filePath);
        qlPreview.DataSource = new PreviewControllerDS(item);
        currentController.PresentViewController((UIViewController)qlPreview, true, (Action)null);
    }

    private string GetMimeType(string filename)
    {
        if (string.IsNullOrEmpty(filename))
        {
            return null;
        }

        var extension = Path.GetExtension(filename.ToLowerInvariant());

        switch (extension)
        {
            case "png":
                return "image/png";
            case "doc":
                return "application/msword";
            case "pdf":
                return "application/pdf";
            case "jpeg":
            case "jpg":
                return "image/jpeg";
            case "zip":
            case "docx":
            case "xlsx":
            case "pptx":
                return "application/zip";
            case "htm":
            case "html":
                return "text/html";
        }
        return "application/octet-stream";
    }
}
{% endhighlight %}
{% endtabs %}

A complete working example of creating an Excel document in the .NET MAUI application can be downloaded from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/ze/MAUISample-523212596.zip).

By executing the program in windows, you will get the **Excel document** as follows.

![.NET MAUI Desktop output Excel document](MAUI_images/MAUI_images_img4.png)

## Read and Edit Excel file

The below code snippet illustrates how to read and edit an Excel file in .NET MAUI.

{% tabs %}
{% highlight C# %}
//Create an instance of ExcelEngine.
using (ExcelEngine excelEngine = new ExcelEngine())
{
    IApplication application = excelEngine.Excel;
    application.DefaultVersion = ExcelVersion.Xlsx;

    Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
    Stream inputStream = executingAssembly.GetManifestResourceStream("MAUISample.Sample.xlsx");

    //Create a workbook with a worksheet
    IWorkbook workbook = application.Workbooks.Open(inputStream);

    //Access first worksheet from the workbook instance.
    IWorksheet worksheet = workbook.Worksheets[0];

    //Set Text in cell A3.
    worksheet.Range["A3"].Text = "Hello World";

    MemoryStream ms = new MemoryStream();
    workbook.SaveAs(ms);
    ms.Position = 0;
	
    //Saves the memory stream as a file.
    DependencyService.Get<ISave>().SaveAndView("Invoice.xlsx", "application/excel", ms);
}
{% endhighlight %}
{% endtabs %}

N> Starting with v16.2.0.x, if you reference Syncfusion assemblies from trial setup or from the NuGet feed, you also have to add "Syncfusion.Licensing" assembly reference and include a license key in your projects. Please refer to this [link](https://help.syncfusion.com/common/essential-studio/licensing/license-key) to know about registering Syncfusion license key in your applications to use our components.
