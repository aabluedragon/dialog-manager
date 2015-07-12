# dialog-manager
A dialog manager for Polymer's paper-dialog.

Install by running
`bower install aabluedragon/dialog-manager`, then import dialog-manager by adding it to your html:
`<link rel="import" href="../bower_components/dialog-manager/dialog-manager.html">`

dialog-manager's purpose is to allow you to create polymer paper dialogs programmatically, which grants you the ability to easily modify your dialogs by code, and even show multiple dialogs.

If you have used [angular material dialogs](https://material.angularjs.org/latest/#/demo/material.components.dialog), the syntax should be familiar to you.

Simple dialog example:
Place the elment in your html: `<dialog-manager id="dm"></dialog-manager>`.
`this.$.dm.start().title('Hello').body('I am your body').confirm('Ah... Ok').open();`

