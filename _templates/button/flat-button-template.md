#intro
This help article shows how you can setup **@{control}** with **Material** **Skin** to render it as flat button. 

Flat button is styled with no background color. You can see an example in **Figure 1**

>important Flat button style is available only with **Material** **Skin**. 

In order to render such a button you should add the @{className} class to the {% if '@{control}' == 'RadFormDecorator' %} button element {%else%} control {%endif%} so to get the proper styles. You can see **Example 1**.

>caption Figure 1: Flat button style vs normal button style.

![](images/flat-button.png)

>caption Example 1: Rendering flat button with @{control}
#end

#see-also
{%if '@{exclude}' != 'RadButton'%}
* [RadButton: Flat Button]({%slug button/appearance-and-styling/flat-button%})
{%endif%}

{%if '@{exclude}' != 'RadPushButton'%}
* [RadPushButton: Flat Button]({%slug pushbutton/appearance-and-styling/flat-button%})
{%endif%}

{%if '@{exclude}' != 'RadLinkButton'%}
* [RadLinkButton: Flat Button]({%slug linkbutton/appearance-and-styling/flat-button%})
{%endif%}

{%if '@{exclude}' != 'RadFormDecorator'%}
* [RadFormDecorator: Flat Button]({%slug formdecorator/appearance-and-styling/flat-button%})
{%endif%}
#end



