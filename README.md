# dialog-manager
A dialog manager for [Polymer](https://www.polymer-project.org)'s [paper-dialog](https://elements.polymer-project.org/elements/paper-dialog?active=paper-dialog&view=demo:demo/index.html).

Install by running
`bower install aabluedragon/dialog-manager --save`, then import dialog-manager by adding it to your html:
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

`start()` begins the dialog constuction, `open()` returns a reference to the constructed paper-dialog so you can manipulate it later, while you could also call build() first, which also returns it, and then call open() after you have finished preparing the dialog:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').build().open();
```

To get a reference to your dialog, you could use both `build` or `open`, for example:
```javascript
var dialog = this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').open();
dialog.close() // The use will see nothing, because we have opened and closed the dialog immediately.
```
Note that after a dialog has finished it's process, the dialog-manager removes it from the DOM completely for convenience.

For convenience, you can have a callback for once the dialog has been closed:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').dismiss('Nah').open(function(arg){
   console.log("iron-overlay-closed has been triggered");
   if(arg.detail.confirmed === false) {
     console.log('Class dismissed');
   }
});
```
Note: if you called `build` before open, then `build` takes the callback instead of `open`.

You can add a dismiss button:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').dismiss('No thanks').open();
```

Creating a dialog using plain HTML as the content:
```javascript
this.$.dm.start().html(`
      <h2>Dialog Title</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
      <div class="buttons">
        <paper-button >More Info...</paper-button>
        <paper-button dialog-dismiss>Decline</paper-button>
        <paper-button dialog-confirm autofocus>Accept</paper-button>
      </div>`).open();
```
Note that you should send the HTML string without the `<paper-dialog>...</paper-dialog>` part.

Appending HTML to the bottom of the dialog:
```javascript
this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').dismiss('No thanks').appendHtml("<div>Extra content</div>").open();
```
Note that as opposed to `appendHtml()`, the `html()` function prepends your html content.

Create a spinner dialog:
```javascript
this.$.dm.start().spinner().dismiss('Cancel').open();
```
Note that adding a spinner implicitly adds a `modal="true"` attribute to your dialog to prevent closing it by clicking outside the dialog box.

Adding default attributes to your dialog-manager, which will be stamped for each paper-dialog it creates:
```javascript
this.$.dm.defaultAttributes = {
         'entry-animation':'scale-up-animation',
         'with-backdrop':'true',
         'exit-animation':'fade-out-animation'
      };
```

Adding attributes to your paper-dialog:
```javascript
this.$.dm.start().title('Title').body('Body').confirm('Mkay').attrs({
         'entry-animation':'scale-up-animation',
         'with-backdrop':'true',
         'exit-animation':'fade-out-animation'
      }).open();
```
Note that adding attributes like that will make the dialog-manager ignore it's `defaultAttributes` for that particular dialog.

Removing all open dialogs:
```javascript
this.$.dm.removeAllDialogs();
```

Retreiving all open dialogs:
```javascript
var allOfEm = this.$.dm.getAllDialogs();
```
