<img src="https://img.shields.io/badge/Android_Studio-v4.0.1-blue"> 

# A-Kart - <i>The Agnel Stores App</i> 

A-Kart is an android application that was developed for our college stationary stores.It consists of 2 apps namely 1.A student app and 2. An admin app for validation.
Students can add the items to purchase to the cart. The administrator can verify the student purchases by scanning the unique QR code genenrated in the student app.<br><br>
<i>myapp</i> is the Student application and <i>Akart_Admin</i> is the admin android application

# Working
New users have to sign-up for a new account. The users will be added to the users collection in google firebase 


After the user saves the cart list, the item details are stored in a collection named Items
```java
final DocumentReference documentRef = fstore.collection("Items").document(userID);
  add.setOnClickListener(new View.OnClickListener() {
  .
  .
  items.put(product_item, total);
  documentRef.set(items);
  .
  .
  }
```

The QR code is generated using the following code.
```java
UserId = FirebaseAuth.getInstance().getCurrentUser().getUid();
qrgEncoder = new QRGEncoder(UserId, null, QRGContents.Type.TEXT,smallerdimension);
try{
            bitmap = qrgEncoder.encodeAsBitmap();
            qrcode.setImageBitmap(bitmap);
}
```
<br>

The Admin app scans the Qr-Code and extracts the UserID:
```java 
scan.setOnClickListener(new View.OnClickListener() {
@Override
public void onClick(View v) {
qrScan.initiateScan();
}
```
Once userID is got it searches the database for the document
```java
qrText = result.getContents().trim();
DocumentReference documentReference = firebaseFirestore.collection("Items").document(qrText);
DocumentReference doc = firebaseFirestore.collection("Users").document(qrText);
```
