# JS-undo-redo
Undo, Redo and persistence implementation with JS in the browsers utilizing the HTML5 Localstorage

This is a very small (around 100 lines) javascript library that allows taking advantage of the HTML5 Localstorage to implement undo, redo and persistence of data on pages.

## How it started

I was creating a data entry form for our expense records. I found out quickly that accidental deletions, closing the tab, etc could be very annoying and time consuming because of the loss of data which then has to be typed back in.

So, I thought: how about saving the state of the entry form on a regular basis and be able to undo and redo. Also, if the tab or browser window was closed, I could get the last saved state back.

## How to Use it

1. load the JS file, or include it your another JS file of yours (since it's so small)
2. initialize the undo-redo object:
  
  `var myUndoRedo=undoRedo(10,_object_to_save_or_restore)`

  Where `10` is the max number of states to save, and the second parameter is the object that will be saved and restored by undoRedo.
  
  The initialization will reload the values into the given object if there's anything in the localstorage from the last time.
3. In your application, call the following functions when needed:
  
  `myUndoRedo.save() //to save a state`

  `myUndoRedo.undo() //to restore one step back`
  
  `myUndoRedo.redo() //to undo an undo :-)`
  
  `myUndoRedo.clear() //to remove all previously saved states`
  
  `myUndoRedo.hasUndo() //returns true if there's a state to go back to`
  
  `myUndoRedo.hasRedo() //returns true if there's a state to do a redo operation`

## Use cases

This little library was developed to be used with other libraries that create 2-way binding to HTML input elements. It's tested with RactiveJS but should work with AngularJS and other libraries of similar kind.

However, it can be used in itself if the all state variables that your app uses are in a single object.

## Limitations

- Due to browser limitation for the amount of data allocated to localstorage the number of states you can save might be less than what you specified, especially if the object you are saving is large.
- Fuction values won't be saved in your object. The states are stored as JSON strings (because localstorage only stores strings), so anything that cannot be serialized will get lost. 
- The library assumes that there's only one undo-redo is needed for one page. So you can't use this to have an undo-redo functionality for two sections separately. If I get requests for that then I'll implement it but this doesn't seem to be needed at the moment

## Future additions (Todos)

- add a timer function(s) to automatically save states in given intervals
- create a demo 
- do a more tests on different scenarios

## Contributions

You can help this make better by
- Testing it in your application(s) and submitting Issue reports
- Pull requests
