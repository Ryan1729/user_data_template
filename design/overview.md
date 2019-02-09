### How I want it to work

#### End-User
There is a download button and an upload button I know where to find. The download button lets me backup my save file. The upload button lets me overwrite the save file with my own previous version. It shouls tell me some things about the current saved file. Like when it was last saved, and how big it is, so I can know which one I loaded.

#### Template User

I want a save and load function that I can call to save stuff and load stuff respectively. I want an interface for the user I don't need to touch, but which I can move around and style if I want to. It should be hideable by default so the impact on my app's look is minimal. Users should know how to use it though, so it should be self explanatory. I guess this means a small label you can know what it is, and a control that makes it obvious you can click it. But, I should be able to completely rip apart and replace this interface and not have to do anything besides hook up some callbacks.

____

So How should it work then?

First the saving and loading API: All functions should be on an object which we return from an init function.

`save` : takes a string and saves it to local storage and calls `onFileChange`.
`load` : returns a string, (possible empty but always a string) from local storage and calls `onFileChange`.

I'm thinking we make the example interface and use the following functions to make it:

`saveButton` : the `onClick` for a save button. Calls `onFileChange`.
`loadButton` : the `onClick` for a load button. Calls `onFileChange`.
`onFileChange` : a callback that is called with the file when the file changes, either from saving or loading by the end-user or when the `save` and `load` buttons are used. A second parameter will be the string key of the function that caused it to happen.

We then provide a helper function `getFileStats` which takes a file and returns an object with the file stats and we will use `onFileChange` and this function to update the file stats for the user.

