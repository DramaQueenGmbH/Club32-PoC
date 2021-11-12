# Club23 PoC 

Prototype `SWT.Browser` and Club23 integration

## Purpose

Solve technical challenges when communicating between a webpage embedded in an `SWT.Browser` widget and the hosting Java application.

## Running the app

Clone the project and open it in IntelliJ.
Navigate to the [App class](src/main/java/com/dramaqueen/club23/App.java).
Click the green Play button besides the `main()` method. On macOS, this should likely fail on the first try.
But it created a Run-Configuration which you can now edit.
Use the `Add VM Options` feature and add the following parameter:

`-XstartOnFirstThread`

## Repo layout

The webpage which is loaded into the `SWT.Browser` is located in [`index.html`](src/main/resources/com/dramaqueen/club23/ui/index.html).
It contains anchor tags with special links starting with `dq://`.
A `LocationListener` is registered on the `SWT.Browser` reacting on navigation events from these links.
A global [`FocusManager`](src/main/java/com/dramaqueen/club23/ui/FocusManager.java) is instructed to give keyboard focus to text fields with certain names contained in certain panels.

The values of [`Properties`](src/main/java/com/dramaqueen/club23/model/Property.java) from the Java [`Document`](src/main/java/com/dramaqueen/club23/model/Document.java) can also flow into the webpage.
This is achieved by registering a [`DocumentListener`](src/main/java/com/dramaqueen/club23/model/DocumentListener.java) and then executing a Javascript function defined in `index.html`.
This function tries to find a DOM element with an id matching the `Property` name.
The `.innerHTML` of the DOM element is then set to the value of the `Property`.
