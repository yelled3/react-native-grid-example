# React Native - Grid Layout Example

![](https://raw.githubusercontent.com/yelled3/react-native-grid-example/master/demo.gif)

By default React Native's [ListView](https://facebook.github.io/react-native/docs/listview.html) renders as a table.

In order to change the table layout to a grid layout (similar to [UICollectionViewFlowLayout](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UICollectionViewFlowLayout_class/index.html)) you need to do the following;

### Setup the `ListView` container style
A `ListView` root element is a [ScrollView](https://facebook.github.io/react-native/docs/scrollview.html) that inherits the ListView's `props`:

```js
    var ListView = React.createClass({
    // ...
        render: function() {
            return (
              <ScrollView {...props}
                ref={SCROLLVIEW_REF}>
                {header}
                {bodyComponents}
                {footer}
              </ScrollView>
            );
        }
    }
```
> see [source](https://github.com/facebook/react-native/blob/master/Libraries/CustomComponents/ListView/ListView.js#L363-L370)

With that in mind you can use the ScrollView's [contentContainerStyle](https://facebook.github.io/react-native/docs/scrollview.html#contentcontainerstyle) prop to style the ListView;
```js
var GridLayoutExample = React.createClass({
// ...
render: function() {
    return (
      <ListView contentContainerStyle={styles.list}
        dataSource={this.state.dataSource}
        renderRow={(rowData) => <Text style={styles.item}>{rowData}</Text>}
      />
    );
  }
```

### Define the grid layout using flexbox
Using basic `flexbox` we can define whatever grid layout we want;
```js
var styles = StyleSheet.create({
    list: {
        justifyContent: 'center',
        flexDirection: 'row',
        flexWrap: 'wrap'
    },
    item: {
        backgroundColor: '#CCC',
        margin: 10,
        width: 100,
        height: 100
    }
});
```
If you're `flexbox` is somewhat rusty, I highly recommend you go through [this guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 



## Credits & References
* This example was based on Colin Ramsay's [suggestion on StackoverFlow](http://stackoverflow.com/questions/29394297/listview-grid-in-react-native/29395686#29395686)
* This is a follow up the disucction started on https://github.com/facebook/react-native/issues/1276
* The example code was based on [ListView example](https://github.com/facebook/react-native/blob/master/Examples/UIExplorer/ListViewExample.js), included in the ReactNative's `UIExplorer` examples.
