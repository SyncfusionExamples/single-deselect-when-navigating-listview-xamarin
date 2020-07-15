# How to achieve SingleDeSelect when use ListView with Rg.Plugin.Popup in Xamarin.Forms (SfListView)

You can deselect the [ListViewItem](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.ListViewItem.html) when navigating back to ListView page in Xamarin.Forms [SfListView](https://help.syncfusion.com/xamarin/listview/overview).

You can also refer the following article.

https://www.syncfusion.com/kb/11739/how-to-achieve-singledeselect-when-use-listview-with-rg-plugin-popup-in-xamarin-forms

**XAML**

Bind [SfListView.TapCommand](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~TapCommand.html) to show the Popup page using [Rg.Plugin.Popup](https://github.com/rotorgames/Rg.Plugins.Popup) framework. Bind [SelectedItem](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.SfListView.XForms~Syncfusion.ListView.XForms.SfListView~SelectedItem.html) to handle the selection.

``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ListViewXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.ListView.XForms;assembly=Syncfusion.SfListView.XForms"
             x:Class="ListViewXamarin.MainPage" Title="ListViewPage">

    <ContentPage.BindingContext>
        <local:ContactsViewModel/>
    </ContentPage.BindingContext>

    <ContentPage.Content>
        <syncfusion:SfListView x:Name="listView" ItemSize="60" TapCommand="{Binding ShowPopup}" ItemsSource="{Binding contactsinfo}" SelectedItem="{Binding SelectedItem, Mode=TwoWay}">
            <syncfusion:SfListView.ItemTemplate >
                <DataTemplate>
                    <Grid x:Name="grid">
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="70" />
                            <ColumnDefinition Width="*" />
                        </Grid.ColumnDefinitions>
                        <Image Source="{Binding ContactImage}" VerticalOptions="Center" HorizontalOptions="Center" HeightRequest="50" WidthRequest="50"/>
                        <Grid Grid.Column="1" RowSpacing="1" Padding="10,0,0,0" VerticalOptions="Center">
                            <Label LineBreakMode="NoWrap" TextColor="#474747" Text="{Binding ContactName}"/>
                            <Label Grid.Row="1" Grid.Column="0" TextColor="#474747" LineBreakMode="NoWrap" Text="{Binding ContactNumber}"/>
                        </Grid>
                    </Grid>
                </DataTemplate>
            </syncfusion:SfListView.ItemTemplate>
        </syncfusion:SfListView>
    </ContentPage.Content>
</ContentPage>
```
You can refer to our online document to work with **Rg.Plugin.Popup** using the following link,

[https://www.syncfusion.com/kb/11353/how-to-show-xamarin-forms-listview-sflistview-in-popup-using-rg-plugin-popup-framework](https://www.syncfusion.com/kb/11353/how-to-show-xamarin-forms-listview-sflistview-in-popup-using-rg-plugin-popup-framework)

**C#**

In the **ShowPopup** command, show the Popup page using **PushAsync** method of the [PopupNavigation](https://github.com/rotorgames/Rg.Plugins.Popup/wiki/Navigation) service.

``` c#
public class ContactsViewModel : INotifyPropertyChanged
{
    public Command<object> ShowPopup { get; set; }
    public ContactsViewModel()
    {
        ShowPopup = new Command<object>(ShowPopupPage);
    }
 
    private async void ShowPopupPage(object sender)
    {
        //Setting binding context for the popup page to show the tapped item.
        var popupPage = new ListViewPage();
        popupPage.BindingContext = this;
        await PopupNavigation.Instance.PushAsync(popupPage);
    }
}
```

**Output**

![SingleDeSelectNavigation](https://github.com/SyncfusionExamples/single-deselect-when-navigating-listview-xamarin/blob/master/ScreenShot/SingleDeSelectNavigation.gif)
