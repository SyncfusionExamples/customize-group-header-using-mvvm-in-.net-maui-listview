# How to customize group header using MVVM in .NET MAUI ListView(SfListView)?

In [.NET MAUI ListView](https://www.syncfusion.com/maui-controls/maui-listview), you can customize the [GroupHeaderTemplate](https://help.syncfusion.com/cr/maui/Syncfusion.Maui.ListView.SfListView.html#Syncfusion_Maui_ListView_SfListView_GroupHeaderTemplate) by binding properties in the `ViewModel` to elements within the template. This approach allows elements to be shown or hidden dynamically based on `ViewModel` properties, which will automatically update the UI when these properties change at runtime.

Create a `ViewModel` with a property that can be bound to the `IsVisible` property of elements in the `GroupHeaderTemplate`. Implement `INotifyPropertyChanged` to notify the UI of changes.

**C#**
```
public class ContactsViewModel : INotifyPropertyChanged
{
    private bool isLabelVisible = false;
    public bool IsLabelVisible
    {
        get { return isLabelVisible; }
        set
        {
            isLabelVisible = value;
            OnPropertyChanged("IsLabelVisible");
        }
    }
}
```

**XAML**
```
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:YourNamespace"
             xmlns:listView="clr-namespace:Syncfusion.Maui.ListView;assembly=Syncfusion.Maui.ListView"
             x:Class="YourNamespace.MainPage">
    
    <ContentPage.BindingContext>
        <local:ContactsViewModel />
    </ContentPage.BindingContext>
    
    <ContentPage.Resources>
        <DataTemplate x:Key="GroupHeaderTemplate">
            <ViewCell>
                <ViewCell.View>
                    <Grid>
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="30" />
                            <ColumnDefinition Width="*" />
                            <ColumnDefinition Width="40" />
                        </Grid.ColumnDefinitions>
                        <Image x:Name="NormalImage" Grid.Column="0" HorizontalOptions="Center"
                               Source="{Binding IsExpand, Converter={StaticResource BoolToImageConverter}}"
                               VerticalOptions="Center" />
                        <Label x:Name="label" Text="{Binding Key}" Grid.Column="1" 
                               IsVisible="{Binding Source={x:Reference listView}, Path=BindingContext.IsLabelVisible}" />
                    </Grid>
                </ViewCell.View>
            </ViewCell>
        </DataTemplate>
    </ContentPage.Resources>
    
    <listView:SfListView x:Name="listView" GroupHeaderTemplate="{StaticResource GroupHeaderTemplate}">
        <!-- Other ListView properties and configurations here -->
    </listView:SfListView>
</ContentPage>
```

**Conclusion**

I hope you enjoyed learning how to customize the group header template using MVVM in .NET MAUI ListView.

You can refer to our [.NET MAUI ListView feature tour](https://www.syncfusion.com/maui-controls/maui-listview) page to know about its other groundbreaking feature representations and [documentation](https://help.syncfusion.com/maui/listview/getting-started), and how to quickly get started with configuration specifications. Explore our [.NET MAUI ListView example](https://github.com/syncfusion/maui-demos/tree/master/MAUI/ListView) to understand how to create and manipulate data.

You can check out our components from the [License and Downloads](https://www.syncfusion.com/sales/teamlicense) page for current customers. If you are new to Syncfusion®, try our 30-day [free trial](https://www.syncfusion.com/downloads/maui) to check out our other controls.

Please let us know in the comments section below if you have any queries or require clarification. You can also contact us through our [support forums](https://www.syncfusion.com/forums), [Direct-Trac](https://support.syncfusion.com/create), or [feedback portal](https://www.syncfusion.com/feedback/maui?control=sflistview). We are always happy to assist you!
