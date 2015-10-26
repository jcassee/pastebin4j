# PasteBin4j
[![PayPayl donate button](http://img.shields.io/paypal/donate.png?color=yellow)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=CR4K3FDKKK5FA&lc=BR&item_name=Kennedy%20Oliveira&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted "Donate with paypal if you feels like helping me out :D")

#### Paste bin API Implementation for Java

Super simples and efficient library implementing all the options provided by the PasteBin api.

With this library you can easily:

- Create pastes for users and as a Guest
- Delete pastes
- List users pastes
- Fetch user information
- Create User Session Key (Actually you doens't need to do that, the library will handle it, but if you want you can create too)
- Get pastes contents (Currently just **PUBLIC** or **UNLISTED** pastes, **PRIVATE** pastes are not supported)

## Maven Support

I'm working on it, maybe more 1 or 2 days and i'll release it into Maven repository, currently you'll need to download a copy of source and build it for you.

## Requeriments

To use the APi you'll need to have a developer key, that you can get from the PasteBin site, you go to this link: [Developer Key](http://pastebin.com/api#1).

## Examples

### Core class
All the interaction is provided by the `PasteBin` class, you need to create one passing your credentials and that is it!

#### Listing your pastes:

````
// Configuration for the Credentials
final String devKey = "dev-key";
final String userName = "user-name";
final String password = "password";

// Create a PasteBin object with the credentials
final PasteBin pasteBin = new PasteBin(new AccountCredentials(devKey, userName, password));

// List all the pastes from the user!
// Pretty easy, isn't?
final List<Paste> pastes = pasteBin.listUserPastes();

// The method nevers returns null, so you can check if the list is empty to see if you have pastes or not
if (pastes.isEmpty()) {
    System.out.println("You don't have any pastes :(");
    return;
}

// Getting a paste
final Paste paste = pastes.get(0);

// Current info on pastes
System.out.println("Title: " + paste.getTitle());
System.out.println("Visibility: " + paste.getVisibility().name());
System.out.println("Unique Key: " + paste.getKey());
System.out.println("Sintax Highlight: " + paste.getHighLight().name());
System.out.println("Paste Date: " + paste.getLocalPasteDate());
System.out.println("Paste Expiration: " + paste.getExpiration());
System.out.println("Paste Expiration Date: " + paste.getLocalExpirationDate());
System.out.println("Hits: " + paste.getHits());
System.out.println("URL:  " + paste.getUrl());
System.out.println("Size: " + paste.getSize());

// Prints all information of all pastes
pastes.forEach(System.out::println);
````

#### Creating a new Paste

````
final String devKey = "dev-key";
final String userName = "user-name";
final String password = "password";

final PasteBin pasteBin = new PasteBin(new AccountCredentials(devKey, userName, password));

//  Basic creation
final Paste paste = new Paste();

paste.setTitle("Testing API");
paste.setExpiration(PasteExpiration.ONE_HOUR);
paste.setHighLight(PasteHighLight.Java);
paste.setVisibility(PasteVisibility.UNLISTED);
paste.setContent("public class Teste { }");

final String url = pasteBin.createPaste(paste);

System.out.println("Paste created at url: " + url);
````

The api gives you enums with all the information so you can just select it easy, doens't need to remember, the class `PasteHighLight` has all the SintaxHighLight currently implemented in the PasteBin, the class `PasteExpiration` has all the possible values for Expiration in a Paste and the `PasteVisibility` has the visibility status of a paste.

You can create a guest Paste by using a `GuestPaste` instead of a paste.

````
Paste p = new GuestPaste();
````

Even if you specify your `username` and `password` using this class your paste will be created as guest.

There are builder for creating the pastes that you can access by `Paste.newBuilder()`.

### More examples
Check the `src/examples` for more examples, there you can see how to list trends pastes, get user information and more!

### Contribution
If you want to contrib you can fork the project and send pull requests, you can even provide your own implementation of the API just by creating a class that implements the `PasteBinApi` interface and pass it to the `PasteBin` constructor.

### Problems & Sugestions
If you enconter any problem, please report at [Issues](https://github.com/kennedyoliveira/pastebin4j/issues) i'm work on it the fast as i can.

## License
This project is licensed with MIT License, so you can freely use, modify and distribute.

## Donations
If this projects helped you and you feels like helping me back, consider a donation, it'll help me alot!
Anyway, if this helped you i'm glad i could help you!
