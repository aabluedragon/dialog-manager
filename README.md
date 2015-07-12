# dialog-manager
A dialog manager for Polymer's paper-dialog.

Install by running
`bower install aabluedragon/dialog-manager`, then import dialog-manager by adding it to your html:
`<link rel="import" href="../bower_components/dialog-manager/dialog-manager.html">`

dialog-manager's purpose is to allow you to create polymer paper dialogs programmatically, which grants you the ability to easily modify your dialogs by code, and even show multiple dialogs.

If you have used [angular material dialogs](https://material.angularjs.org/latest/#/demo/material.components.dialog), the syntax should be familiar to you.

Simple dialog example:
Place the element in your html: 
```html
<dialog-manager id="dm"></dialog-manager>
```
Then call
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').open();
```

start() beins the dialog constuction, open() returns a reference to the constructed paper-dialog so you can manipulate it later, while you could also call build() first, which also returns it, and then call open() after you have finished preparing the dialog:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').build().open();
```

For convenience, you can have a callback for once the dialog has been closed:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').open(function(arg){
   console.log("iron-overlay-closed has been triggered");
   if(arg.detail.confirmed === false) {
     console.log('Class dismissed');
   }
});
```
Note: if you called `build` before open, the the `build` function takes the callback instead of `open`.

You can add a dismiss button:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').dismiss('No thanks').open();
```
