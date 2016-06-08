---
title: OnExportContent
page_title: OnExportContent | RadEditor for ASP.NET AJAX Documentation
description: OnExportContent
slug: editor/server-side-programming/events/onexportcontent
tags: onexportcontent
published: True
position: 0
---

# OnExportContent

The **OnExportContent** event fires just before the content from the **Telerik Editor** is exported. It provides access to the generated output, so that it could be used or modified upon further application requirements.

The event handler receives two arguments:

1. **Sender**–the **RadEditor** instance that raised the event.

1. **Event arguments**–an object of type [Telerik.Web.UI.EditorExportingArgs](http://www.telerik.com/help/aspnet-ajax/t_telerik_web_ui_editorexportingargs.html) exposes the string **ExportOutput** property, the [Telerik.Web.UI.ExportType ](www.telerik.com/help/aspnet-ajax/t_telerik_web_ui_exporttype.html) **ExportType** property and a **Boolean Cancel** property with which you can	cancel the sending of the file to the client (by default is set to *false*).

>caption Example 1: How to save the **ExportOutput** to a file on the server and prevent it from being sent to the client.

````ASP.NET
<telerik:RadEditor RenderMode="Lightweight" runat="server" ID="RadEditor1" OnExportContent="RadEditor1_ExportContent" ContentFilters="DefaultFilters, PdfExportFilter">
</telerik:RadEditor>
<asp:Button runat="server" ID="Button1" Text="Export to PDF" OnClick="Button1_Click" />
````
````C#
using System;
using System.IO;
using Telerik.Web.UI;

public partial class DefaultCS : System.Web.UI.Page
{
	protected void RadEditor1_ExportContent(object sender, EditorExportingArgs e)
	{
		string url = String.Format("~/{0}.pdf", RadEditor1.ExportSettings.FileName);
		string path = Server.MapPath(url);

		if (File.Exists(path))
		{
			File.Delete(path);
		}

		using (FileStream fs = File.Create(path))
		{
			Byte[] info = System.Text.Encoding.Default.GetBytes(e.ExportOutput);
			fs.Write(info, 0, info.Length);
		}

		e.Cancel = true;
	}

	protected void Button1_Click(object sender, EventArgs e)
	{
		RadEditor1.ExportToPdf();
	}
}
````
````VB
Imports System.IO
Imports Telerik.Web.UI

Partial Class DefaultVB
	Inherits System.Web.UI.Page

	Protected Sub RadEditor1_ExportContent(sender As Object, e As EditorExportingArgs)
		Dim url As String = String.Format("~/{0}.pdf", RadEditor1.ExportSettings.FileName)
		Dim path As String = Server.MapPath(url)

		If File.Exists(path) Then
			File.Delete(path)
		End If

		Using fs As FileStream = File.Create(path)
			Dim info As [Byte]() = System.Text.Encoding.[Default].GetBytes(e.ExportOutput)
			fs.Write(info, 0, info.Length)
		End Using

		e.Cancel = True
	End Sub

	Protected Sub Button1_Click(sender As Object, e As EventArgs)
		RadEditor1.ExportToPdf()
	End Sub
End Class
````

>caption Example 2: Dynamically adding header and footer elements to the exported document in the **OnExportContent** event.

````ASP.NET
<telerik:RadEditor RenderMode="Lightweight" runat="server" ID="RadEditor1" OnExportContent="RadEditor1_ExportContent" ContentFilters="DefaultFilters, PdfExportFilter"></telerik:RadEditor>
<asp:Button runat="server" ID="Button1" Text="Export to DOCX" OnClick="Button1_Click" />
````
````C#
using System.Linq;
using System.Text;
using Telerik.Web.UI;
using Telerik.Windows.Documents.Flow.FormatProviders.Docx;
using Telerik.Windows.Documents.Flow.Model;
using Telerik.Windows.Documents.Flow.Model.Styles;

public partial class DefaultCS : System.Web.UI.Page
{
	protected void RadEditor1_ExportContent(object sender, EditorExportingArgs e)
	{
		ExportType exportType = e.ExportType;

		if (exportType == ExportType.Word)
		{
			string exportedOutput = e.ExportOutput;

			Byte[] output = Encoding.Default.GetBytes(exportedOutput);

			DocxFormatProvider docxProvider = new DocxFormatProvider();
			RadFlowDocument document = docxProvider.Import(output);

			Header defaultHeader = document.Sections.First().Headers.Add();
			Paragraph defaultHeaderParagraph = defaultHeader.Blocks.AddParagraph();
			defaultHeaderParagraph.TextAlignment = Alignment.Right;
			defaultHeaderParagraph.Inlines.AddRun("This is a sample header.");

			Footer defaultFooter = document.Sections.First().Footers.Add();
			Paragraph defaultFooterParagraph = defaultFooter.Blocks.AddParagraph();
			defaultFooterParagraph.TextAlignment = Alignment.Right;
			defaultFooterParagraph.Inlines.AddRun("This is a sample footer.");

			Byte[] modifiedOutput = docxProvider.Export(document);
			string finalOutput = Encoding.Default.GetString(modifiedOutput, 0, modifiedOutput.Length);

			e.ExportOutput = finalOutput;
		}
	}

	protected void Button1_Click(object sender, EventArgs e)
	{
		RadEditor1.ExportToDocx();
	}
}
````
````VB
Imports Telerik.Web.UI
Imports Telerik.Windows.Documents.Flow.FormatProviders.Docx
Imports Telerik.Windows.Documents.Flow.Model
Imports Telerik.Windows.Documents.Flow.Model.Styles

Partial Class DefaultVB
	Inherits System.Web.UI.Page

	Protected Sub RadEditor1_ExportContent(sender As Object, e As EditorExportingArgs)
		Dim exportType**1 As ExportType = e.ExportType

		If exportType**1 = ExportType.Word Then
			Dim exportedOutput As String = e.ExportOutput

			Dim output As [Byte]() = Encoding.[Default].GetBytes(exportedOutput)

			Dim docxProvider As New DocxFormatProvider()
			Dim document As RadFlowDocument = docxProvider.Import(output)

			Dim defaultHeader As Header = document.Sections.First().Headers.Add()
			Dim defaultHeaderParagraph As Paragraph = defaultHeader.Blocks.AddParagraph()
			defaultHeaderParagraph.TextAlignment = Alignment.Right
			defaultHeaderParagraph.Inlines.AddRun("This is a sample header.")

			Dim defaultFooter As Footer = document.Sections.First().Footers.Add()
			Dim defaultFooterParagraph As Paragraph = defaultFooter.Blocks.AddParagraph()
			defaultFooterParagraph.TextAlignment = Alignment.Right
			defaultFooterParagraph.Inlines.AddRun("This is a sample footer.")

			Dim modifiedOutput As [Byte]() = docxProvider.Export(document)
			Dim finalOutput As String = Encoding.[Default].GetString(modifiedOutput, 0, modifiedOutput.Length)

			e.ExportOutput = finalOutput
		End If
	End Sub

	Protected Sub Button1_Click(sender As Object, e As EventArgs)
		RadEditor1.ExportToDocx()
	End Sub
End Class
````


## See Also

 * [Import and Export to Word]({%slug editor/functionality/import-and-export/import-and-export-to-word%})

 * [Export to DOCX and RTF]({%slug editor/functionality/import-and-export/export-to-docx-and-rtf%})

 * [Export to PDF]({%slug editor/functionality/import-and-export/export-to-pdf%})
 
 * [Telerik Document Processing - RadWordsProcessing](http://docs.telerik.com/devtools/document-processing/libraries/radwordsprocessing/overview)
 
 * [RadFlowDocument](http://docs.telerik.com/devtools/document-processing/libraries/radwordsprocessing/model/radflowdocument)
