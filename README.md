**[View document in Syncfusion Xamarin Knowledge base](https://www.syncfusion.com/kb/12466/how-to-retain-groups-after-updating-the-itemssource-in-xamarin-forms-listview-using-mvvm)**

## Sample

```xaml
<StackLayout>
    <Button Text="Refresh ItemsSource" Command="{Binding RefreshCommand}" HeightRequest="50"/>
    <syncfusion:SfListView x:Name="listView" ItemSize="60" DataSource="{Binding ListDataSource}" ItemsSource="{Binding ContactsInfo}">
        <syncfusion:SfListView.ItemTemplate >
            <DataTemplate>
                    <code>
                    . . .
                    . . .
                    <code>
            </DataTemplate>
        </syncfusion:SfListView.ItemTemplate>
    </syncfusion:SfListView>
</StackLayout>

C#:

public Command RefreshCommand { get; set; }

RefreshCommand = new Command(RefreshItemsSource);

private void RefreshItemsSource(object obj)
{
    if(ContactsInfo.Count > 0)
    {
        ContactsInfo.Clear();
        ContactsInfo = null;
    }

    GenerateInfo();
    ListDataSource.GroupDescriptors.Add(new GroupDescriptor() { PropertyName = "ContactType" });
}

public void GenerateInfo()
{
    Random r = new Random();
    ContactsInfo = new ObservableCollection<Contacts>();
    for (int i = 0; i < 30; i++)
    {
        var contact = new Contacts(CustomerNames[i], r.Next(720, 799).ToString() + " - " + r.Next(3010, 3999).ToString());
        contact.ContactImage = ImageSource.FromResource("ListViewXamarin.Images.Image" + r.Next(0, 28) + ".png");
        contact.ContactType = contactTypes[r.Next(0, 3)];
        ContactsInfo.Add(contact);
    }
}
```