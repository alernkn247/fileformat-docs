---
title: Mail merge options | Syncfusion
description: This section illustrates how to merge the data from data source to a Word document
platform: file-formats
control: DocIO
documentation: UG
---

# Mail merge options

The MailMerge class allows you to customize the Mail merge process with the following options.

## Field Mapping

The MailMerge class can automatically maps the merge field names with data source column names during Mail merge process. You can also customize the field mapping when the merge field names in the template document varies with the column names in the data source by using MappedFields collection.

The following code example shows how to add mapping when a merge field name in a document and column name in a data source have different names.

{% tabs %}

{% highlight c# %}

//Opens the template document. 

WordDocument document = new WordDocument("Template.docx");

//Creates data source

string[] fieldNames = new string[] { "Employee_Id_InDataSource", "Name_InDataSource", "Phone_InDataSource", "City_InDataSource" };

string[] fieldValues = new string[] { "101", "John", "+122-2000466", "Houston" };

//Mapping the required merge field names with data source column names

document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource");

document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource");

document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource");

document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource");

//Performs the mail merge

document.MailMerge.Execute(fieldNames, fieldValues);

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the template document. 

Dim document As New WordDocument("Template.docx")

'Creates data source

Dim fieldNames As String() = New String() {"Employee_Id_InDataSource", "Name_InDataSource", "Phone_InDataSource", "City_InDataSource"}

Dim fieldValues As String() = New String() {"101", "John", "+122-2000466", "Houston"}

'Mapping the required merge field names with data source column names

document.MailMerge.MappedFields.Add("Employee_Id_InDocument", "Employee_Id_InDataSource")

document.MailMerge.MappedFields.Add("Name_InDocument", "Name_InDataSource")

document.MailMerge.MappedFields.Add("Phone_InDocument", "Phone_InDataSource")

document.MailMerge.MappedFields.Add("City_InDocument", "City_InDataSource")

'Performs the mail merge

document.MailMerge.Execute(fieldNames, fieldValues)

'Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}

## Retrieving the merge field names

The following code example shows how to retrieve the merge field names in the Word document

{% tabs %}

{% highlight c# %}

//Gets the merge field names from the document.
string[] fieldNames = document.MailMerge.GetMergeFieldNames();

{% endhighlight %}

{% highlight vb.net %}

'Gets the merge field names from the document.
Dim fieldNames As String() = document.MailMerge.GetMergeFieldNames()

{% endhighlight %}

{% endtabs %}

The following code example shows how to retrieve the merge field group names in the Word document

{% tabs %}

{% highlight c# %}

//Gets the merge field group names from the document.

string[] groupNames = document.MailMerge.GetMergeGroupNames();

{% endhighlight %}

{% highlight vb.net %}

'Gets the merge field group names from the document.

Dim groupNames As String() = document.MailMerge.GetMergeGroupNames()

{% endhighlight %}

{% endtabs %}

The following code example shows how to retrieve the merge field names for a specific group in the Word document

{% tabs %}

{% highlight c# %}

//Gets the fields from the specified groups. 

string[] fieldNames = document.MailMerge.GetMergeFieldNames(groupName);

{% endhighlight %}

{% highlight vb.net %}

'Gets the fields from the specified groups. 

Dim fieldNames As String() = document.MailMerge.GetMergeFieldNames(groupName)

{% endhighlight %}

{% endtabs %}

## Removing empty paragraphs

The following code example shows how to remove the empty paragraphs when the paragraph has a merge field item without any data during Mail merge process.

{% tabs %}

{% highlight c# %}

//Opens the template document. 

WordDocument document = new WordDocument("Template.docx");

//Removes paragraph that contains only empty fields. 

document.MailMerge.RemoveEmptyParagraphs = true;

string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };

string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };

//Performs the mail merge.

document.MailMerge.Execute(fieldNames, fieldValues);

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the template document. 

Dim document As New WordDocument("Template.docx")

'Removes paragraph that contains only empty fields. 

document.MailMerge.RemoveEmptyParagraphs = True

Dim fieldNames As String() = New String() {"EmployeeId", "Phone", "City"}

Dim fieldValues As String() = New String() {"1001", "+91-9999999999", "London"}

'Performs the mail merge.

document.MailMerge.Execute(fieldNames, fieldValues)

'Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}

## Removing empty merge fields

Essential DocIO removes or keeps the unmerged merge fields in the output document based on the ClearFields property on each mail merge execution.

When a merge field is considered as unmerged during mail merge process?

1.The merge field doesn't have mapping field in data source.

2.The merge field has mapping field in data source, but the data is null or string.Empty.

Mail merge operation automatically removes the unmerged merge fields since the default value of ClearFields property is true.

T> 1.Set ClearFields property as false before the mail merge execution statement. If your requirement is to keep the unmerged merge fields in the output document. 

T> 2.Modify ClearFields property before each mail merge execution statement, while performing multiple mail merge executions. If your requirement is to remove the unmerged merge fields in one mail merge execution and keep the unmerged merge fields in another mail merge execution. 

T> 3.Order the mail merge executions with ClearFields property false as first, to avoid removal merge fields that are required for next mail merge execution in the same document.

The following code example shows how to keep the unmerged merge fields in the generated Word document.
 
{% tabs %}

{% highlight c# %}

//Opens the template document. 

WordDocument document = new WordDocument("Template.docx");

//Sets “ClearFields” to true to remove empty mail merge fields from document. 

document.MailMerge.ClearFields = false;

string[] fieldNames = new string[] { "EmployeeId", "Phone", "City" };

string[] fieldValues = new string[] { "1001", "+91-9999999999", "London" };

//Performs the mail merge.

document.MailMerge.Execute(fieldNames, fieldValues);

//Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx);

document.Close();

{% endhighlight %}

{% highlight vb.net %}

'Opens the template document. 

Dim document As New WordDocument("Template.docx")

'Sets “ClearFields” to true to remove empty mail merge fields from document. 

document.MailMerge.ClearFields = False

Dim fieldNames As String() = New String() {"EmployeeId", "Phone", "City"}

Dim fieldValues As String() = New String() {"1001", "+91-9999999999", "London"}

'Performs the mail merge.

document.MailMerge.Execute(fieldNames, fieldValues)

'Saves and closes the Word document instance

document.Save("Sample.docx", FormatType.Docx)

document.Close()

{% endhighlight %}

{% endtabs %}

## Restart numbering in lists

The following code example shows how to restart the list numbering in a Word documents while performing mail merge and merging multiple Word documents.

{% tabs %}  

{% highlight c# %}

//Loads an existing Word document

WordDocument wordDocument = new WordDocument("Template.docx");

//Sets ImportOptions to restart the list numbering

wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;

//Creates the employee details as “IEnumerable” collection

List<Employee> employeeList = new List<Employee>();

employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));

employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));

employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));

//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection

MailMergeDataTable dataTable = new MailMergeDataTable("Employee", employeeList);

//Performs mail merge

wordDocument.MailMerge.ExecuteGroup(dataTable);

//Saves the Word document

wordDocument.Save("Sample.docx",FormatType.Docx);

//Closes the instance of Word document object

wordDocument.Close();

/// <summary>

/// Represents the helper class to perform mail merge

/// </summary>

public class Employee

{

    public string EmployeeID { get; set; }

    public string EmployeeName { get; set; }

    public string Location { get; set; }

    /// <summary>
    
	/// Represents a constructor to create value for merge fields
    
	/// </summary>    
    
	public Employee(string employeeId, string employeeName, string location)

    {

        EmployeeID = employeeId;

        EmployeeName = employeeName;

        Location = location;

	}

}

{% endhighlight %}

{% highlight vb.net %}

'Loads an existing Word document

Dim wordDocument As WordDocument = New WordDocument("Template.docx")

'Sets ImportOptions to restart the list numbering

wordDocument.ImportOptions = ImportOptions.ListRestartNumbering

'Creates the employee details as “IEnumerable” collection

Dim employeeList As List(Of Employee) = New List(Of Employee)()

employeeList.Add(New Employee("101", "Nancy Davolio", "Seattle, WA, USA"))

employeeList.Add(New Employee("102", "Andrew Fuller", "Tacoma, WA, USA"))

employeeList.Add(New Employee("103", "Janet Leverling", "Kirkland, WA, USA"))

'Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection

Dim dataTable As MailMergeDataTable = New MailMergeDataTable("Employee", employeeList)

'Performs mail merge

wordDocument.MailMerge.ExecuteGroup(dataTable)

'Saves the Word document

wordDocument.Save("Sample.docx", FormatType.Docx)

'Closes the instance of Word document object

wordDocument.Close()

'Represents the helper class to perform mail merge

Public Class Employee

    Public Property EmployeeID() As String

        Get

            Return m_EmployeeID

        End Get

        Set(value As String)

            m_EmployeeID = value

        End Set

    End Property

    Private m_EmployeeID As String

    Public Property EmployeeName() As String

        Get

            Return m_EmployeeName

        End Get

        Set(value As String)

            m_EmployeeName = value

        End Set

    End Property

    Private m_EmployeeName As String

    Public Property Location() As String

        Get

            Return m_Location

        End Get

        Set(value As String)

            m_Location = value

        End Set

    End Property

    Private m_Location As String

    'Represents a constructor to create value for merge fields

    Public Sub New(employeeId As String, employeeName As String, location As String)

        m_EmployeeID = employeeId

        m_EmployeeName = employeeName

        m_Location = location

	End Sub

End Class

{% endhighlight %}

{% highlight ASP.NET CORE %}

FileStream fileStream = new FileStream("Template.docx", FileMode.Open);

//Loads an existing Word document

WordDocument wordDocument = new WordDocument(fileStream, FormatType.Docx);

//Sets ImportOptions to restart the list numbering

wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;

//Creates the employee details as “IEnumerable” collection

List<Employee> employeeList = new List<Employee>();

employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));

employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));

employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));

//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection

MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);

//Performs mail merge

wordDocument.MailMerge.ExecuteGroup(dataTable);

//Saves the Word document

MemoryStream outputStream = new MemoryStream();

wordDocument.Save(outputStream, FormatType.Docx);

//Closes the instance of Word document object

wordDocument.Close();

/// <summary>

/// Represents the helper class to perform mail merge

/// </summary>

public class Employee

{

    public string EmployeeID { get; set; }

    public string EmployeeName { get; set; }

    public string Location { get; set; }

    /// <summary>
    
	/// Represents a constructor to create value for merge fields
    
	/// </summary>    
    
	public Employee(string employeeId, string employeeName, string location)

    {

        EmployeeID = employeeId;

        EmployeeName = employeeName;

        Location = location;

	}

}

{% endhighlight %}

{% highlight XAMARIN %}

//Load the Word document as stream 

Stream docStream = typeof(App).GetTypeInfo().Assembly.GetManifestResourceStream("Sample.Assets.Sample.docx");

// Loads the stream into Word Document

WordDocument wordDocument = new WordDocument(docStream, Syncfusion.DocIO.FormatType.Automatic);

//Sets ImportOptions to restart the list numbering

wordDocument.ImportOptions = ImportOptions.ListRestartNumbering;

//Creates the employee details as “IEnumerable” collection

List<Employee> employeeList = new List<Employee>();

employeeList.Add(new Employee("101", "Nancy Davolio", "Seattle, WA, USA"));

employeeList.Add(new Employee("102", "Andrew Fuller", "Tacoma, WA, USA"));

employeeList.Add(new Employee("103", "Janet Leverling", "Kirkland, WA, USA"));

//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection

MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);

//Performs mail merge

wordDocument.MailMerge.ExecuteGroup(dataTable);

//Saves the Word document.

MemoryStream outputStream = new MemoryStream();

wordDocument.Save(outputStream, FormatType.Docx);

//Closes the instance of Word document object

wordDocument.Close();

/// <summary>

/// Represents the helper class to perform mail merge

/// </summary>

public class Employee

{

	public string EmployeeID { get; set; }
	
	public string EmployeeName { get; set; }
	
	public string Location { get; set; }
	
	/// <summary>
	
	/// Represents a constructor to create value for merge fields
	
	/// </summary>    
	
	public Employee(string employeeId, string employeeName, string location)
	
	{
	
		EmployeeID = employeeId;
	
		EmployeeName = employeeName;
	
		Location = location;
	}
}

{% endhighlight %}

{% endtabs %}

## Insert as new row

The following code example shows how to add each record as new row inside table when the row group contains only one cell, which means, the merge fields denoting group start and end present inside the same cell.

{% tabs %}  

{% highlight C# %}

//Opens the template document. 

WordDocument document = new WordDocument(@"Data/Template.docx");

//Creates a data table.

DataTable table = new DataTable("CompatibleVersions");

table.Columns.Add("WordVersion");

//Creates a new data row.

DataRow row = table.NewRow();

row["WordVersion"] = "Microsoft Word 97-2003";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2007";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2010";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2013";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2019";

table.Rows.Add(row);

//Enable the flag to insert a new row for every group in a table.

document.MailMerge.InsertAsNewRow = true;

//Execute mail merge

document.MailMerge.ExecuteGroup(table);

//Saves and closes the WordDocument instance

document.Save("Sample.docx");

document.Close();

{% endhighlight %}

{% highlight VB.NET %}

'Opens the template document. 

Dim document As WordDocument = New WordDocument("Data/Template.docx")
		
'Creates a data table.

Dim table As DataTable = New DataTable("CompatibleVersions")

table.Columns.Add("WordVersion")
		
'Creates a new data row.

Dim row As DataRow = table.NewRow()

row("WordVersion") = "Microsoft Word 97-2003"

table.Rows.Add(row)

row = table.NewRow()

row("WordVersion") = "Microsoft Word 2007"

table.Rows.Add(row)

row = table.NewRow()

row("WordVersion") = "Microsoft Word 2010"

table.Rows.Add(row)

row = table.NewRow()

row("WordVersion") = "Microsoft Word 2013"

table.Rows.Add(row)

row = table.NewRow()

row("WordVersion") = "Microsoft Word 2019"

table.Rows.Add(row)
		
'Enable the flag to insert a new row for every group in a table.

document.MailMerge.InsertAsNewRow = True
		
'Execute mail merge

document.MailMerge.ExecuteGroup(table)
		
'Saves and closes the WordDocument instance

document.Save("Sample.docx")

document.Close()

{% endhighlight %}

{% highlight ASP.NET CORE %}

//Opens the template document. 

FileStream fileStreamPath = new FileStream(@"Data\Template.docx", FileMode.Open, FileAccess.Read, FileShare.ReadWrite);

WordDocument document = new WordDocument(fileStreamPath, FormatType.Docx);

//Creates a data table. 

DataTable table = new DataTable("CompatibleVersions");

table.Columns.Add("WordVersion");

//Creates a new data row. 

DataRow row = table.NewRow();

row["WordVersion"] = "Microsoft Word 97-2003";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2007";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2010";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2013";

table.Rows.Add(row);

row = table.NewRow();

row["WordVersion"] = "Microsoft Word 2019";

table.Rows.Add(row);
			
//Enable the flag to insert a new row for every group in a table.

document.MailMerge.InsertAsNewRow = true;
			
//Execute mail merge

document.MailMerge.ExecuteGroup(table);

MemoryStream stream = new MemoryStream();

//Saves the Word document to MemoryStream

document.Save(stream, FormatType.Docx);

stream.Position = 0;

//Download Word document in the browser

return File(stream, "application/msword", "Result.docx");

{% endhighlight %}

{% endtabs %}

## Remove empty group

The following code example shows how to remove groups which contain empty merge fields after executing mail merge in a Word document.

{% tabs %}  

{% highlight C# %}

//Opens the template document. 

WordDocument document = new WordDocument(@"Template.docx");

//Gets the employee details as “IEnumerable” collection

List<Employees> employeeList = GetEmployees();

//Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection.

MailMergeDataTable dataTable = new MailMergeDataTable("Employees", employeeList);

//Enable the flag to remove empty group which contain empty merge fields

document.MailMerge.RemoveEmptyGroup = true;

//Performs Mail merge

document.MailMerge.ExecuteNestedGroup(dataTable);

//Saves and closes the WordDocument instance

document.Save("Result.docx");

document.Close();

{% endhighlight %}

{% highlight VB.NET %}

'Opens the template document.

Dim document As WordDocument =  New WordDocument("Template.docx")

'Gets the employee details as “IEnumerable” collection

Dim employeeList As List(Of Employees) =  GetEmployees() 

'Creates an instance of “MailMergeDataTable” by specifying mail merge group name and “IEnumerable” collection.

Dim dataTable As MailMergeDataTable =  New MailMergeDataTable("Employees",employeeList) 

'Enable the flag to remove empty group which contain empty merge fields

document.MailMerge.RemoveEmptyGroup = True

'Performs Mail merge

document.MailMerge.ExecuteNestedGroup(dataTable)

'Saves and closes the WordDocument instance

document.Save("Result.docx")

document.Close() 

{% endhighlight %}