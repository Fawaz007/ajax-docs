---
title: Reordering
page_title: Reordering | RadListBox for ASP.NET AJAX Documentation
description: Reordering
slug: listbox/server-side-programming/server-events/reordering
tags: reordering
published: True
position: 3
---

# Reordering

## 

The **Reordering** server event fires when the **AutoPostBackOnReorder="True"**. It fires once for all selected items.

The event handler receives two parameters:

1. The instance of the listbox firing the event

2. An event arguments parameter containing the following properties:

* **Items** - collection of **RadListBoxItem** objects which were selected for reordering.

* **Offset** - returns **-1** if you are moving the item **up** and **1** if you are moving the item **down**.

* **Cancel** - set it to True to cancel the event and prevent the reordering to happen

The following example shows how to cancel the event if there are more than 2 items to be reordered:

````C#
protected void RadListBox1_Reordering(object sender, RadListBoxReorderingEventArgs e)
{
	if (e.Items.Count > 2)
		e.Cancel = true;
} 
````
````VB.NET
Protected Sub RadListBox1_Reordering(ByVal sender As Object, ByVal e As RadListBoxReorderingEventArgs)
	If e.Items.Count > 2 Then
		e.Cancel = True
	End If
	    End Sub	
````

# See Also

 * [Reordered]({%slug listbox/server-side-programming/server-events/reordered%})

 * [Updating]({%slug listbox/server-side-programming/server-events/updating%})

 * [Updated]({%slug listbox/server-side-programming/server-events/updated%})

 * [Reorder]({%slug listbox/functionality/reorder%})
