---
layout: post
title: Editing with WinUI TreeView control | Syncfusion
description: Learn here about editing of TreeViewNode with Syncfusion WinUI TreeView (SfTreeView) control and editing related events. 
platform: winui
control: SfTreeView
documentation: ug
---

# Editing in WinUI TreeView (SfTreeView)

The TreeView provides support for editing and it can be enabled or disabled by using [SfTreeView.AllowEditing](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_AllowEditing) property.You can enter edit mode in a node by pressing <kbd>F2</kbd> key only. The editing changes in a node will be committed only when user move to next node or pressing <kbd>Enter</kbd> key.

It is necessary to define [EditTemplate](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_EditTemplate) / [EditTemplateSelector](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_EditTemplateSelector) for bound mode, to enable editing. For UnboundMode, textbox will be loaded in edit mode by default.

{% tabs %}
{% highlight xaml %}
<syncfusion:SfTreeView x:Name="treeView"
                        Width="400"
                        Height="500"
                        AutoExpandMode="AllNodes"
                        BorderBrush="LightGray"
                        BorderThickness="1"
                        AllowEditing="True"
                        IsAnimationEnabled="True"
                        ChildPropertyName="Files"
                        ItemsSource="{Binding Folders}">
    <syncfusion:SfTreeView.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <ContentPresenter Width="20"
                                    Height="20"
                                    HorizontalAlignment="Stretch"
                                    VerticalAlignment="Center"
                                    ContentTemplate="{Binding ImageTemplate}" />
                <TextBlock Margin="5"
                            VerticalAlignment="Center"
                            Text="{Binding FileName}" />
            </StackPanel>
        </DataTemplate>
    </syncfusion:SfTreeView.ItemTemplate>
    <syncfusion:SfTreeView.EditTemplate>
        <DataTemplate>
            <TextBox Text="{Binding Name}" 
				VerticalContentAlignment="Center" 
                Margin="-4,0,-4,0"
                Height="{Binding ItemHeight,ElementName=treeView}" />
        </DataTemplate>
    </syncfusion:SfTreeView.EditTemplate>
</syncfusion:SfTreeView>
{% endhighlight %}
{% highlight c# %}
treeView.AllowEditing = true;
{% endhighlight %}
{% endtabs %}

![WinUI TreeView in Edit Mode](Editing-images/Editing-image1.png)

## Programmatic Editing

### Begin the editing

The TreeView allows you to edit the node programmatically by calling the [BeginEdit](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_BeginEdit_Syncfusion_UI_Xaml_TreeView_TreeViewNode_) method.

{% tabs %}
{% highlight c# %}
this.treeView.Loaded += TreeView_Loaded;

private void TreeView_Loaded(object sender, RoutedEventArgs e)
{
    this.treeView.BeginEdit(this.treeView.Nodes[0]);
}
{% endhighlight %}
{% endtabs %}

N> [CurrentItem](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_CurrentItem) is set to the node when the BeginEdit is called.

### End the editing

You can call [EndEdit](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_EndEdit_Syncfusion_UI_Xaml_TreeView_TreeViewNode_) method to programmatically end the editing for specific node.

{% tabs %}
{% highlight c# %}
this.treeView.Loaded += TreeView_Loaded;

private void TreeView_Loaded(object sender, RoutedEventArgs e)
{
    this.treeView.EndEdit(this.treeView.Nodes[0]);
}
{% endhighlight %}
{% endtabs %}

## Events

### ItemBeginEdit Event

The [ItemBeginEdit](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_ItemBeginEdit) event occurs when the node enters edit mode. The [TreeViewItemBeginEditEventArgs](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.TreeViewItemBeginEditEventArgs.html) has the following members which provides information about the `ItemBeginEdit` event.

* [Node](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.TreeViewItemEditEventArgs.html#Syncfusion_UI_Xaml_TreeView_TreeViewItemEditEventArgs_Node) : Gets the [TreeViewNode](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.TreeViewNode.html) which is being edited.

You can cancel the editing of certain nodes using custom logic within this event by setting `TreeViewItemBeginEditEventArgs.Cancel` as true.

{% tabs %}
{% highlight c# %}
treeView.ItemBeginEdit += TreeView_ItemBeginEdit;

private void TreeView_ItemBeginEdit(object sender, Syncfusion.UI.Xaml.TreeView.TreeViewItemBeginEditEventArgs e)
{
    if ((e.Node.Content as Folder).FileName == "Documents")
        e.Cancel = true;
}
{% endhighlight %}
{% endtabs %}

### ItemEndEdit Event

The [ItemEndEdit](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.SfTreeView.html#Syncfusion_UI_Xaml_TreeView_SfTreeView_ItemEndEdit) event occurs when the node leaves the edit mode. The [TreeViewItemEndEditEventArgs](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.TreeViewItemEndEditEventArgs.html) has the following members which provides information about the `ItemEndEdit` event.

* [Node](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.TreeViewItemEditEventArgs.html#Syncfusion_UI_Xaml_TreeView_TreeViewItemEditEventArgs_Node) : Gets the [TreeViewNode](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.TreeView.TreeViewNode.html) which is being edited.

You can cancel the editing from being ended for certain nodes using custom logic within this event by setting `TreeViewItemEndEditEventArgs.Cancel` as true.

{% tabs %}
{% highlight c# %}
treeView.ItemEndEdit += TreeView_ItemEndEdit;

private void TreeView_ItemEndEdit(object sender, TreeViewItemEndEditEventArgs e)
{
    if ((e.Node.Content as Folder).FileName == "Downloads")
        e.Cancel = true;
}
{% endhighlight %}
{% endtabs %}

