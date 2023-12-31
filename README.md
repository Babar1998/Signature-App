<h1><bold>Signature App </bold></h1>


https://github.com/kainatnaeem/Flutter-Signature-App/assets/54583829/e75aec63-2f27-47cf-af61-f32a936ca4dd
# <h1> Create a GlobalKey for SignaturePad: </h1>
# <h4> final GlobalKey<SfSignaturePadState> signaturePadKey = GlobalKey<SfSignaturePadState>();
This key is used to get the state of the SfSignaturePad widget, which allows us to capture the drawn signature. </h4>
# <h1> Add a method to Save Signature:</h1>
# <h4>Future<void> _saveSignature() async {
  // Get the image from the SignaturePad
  ui.Image image = await signaturePadKey.currentState!.toImage();
  // Convert the image to ByteData (binary data)
  ByteData byteData = await image.toByteData(format: ui.ImageByteFormat.png);
  // Convert ByteData to Uint8List (unsigned 8-bit integer list)
  Uint8List uint8List = byteData.buffer.asUint8List();

  // Create a Blob from Uint8List
  final blob = html.Blob([uint8List]);
  // Create a URL for the Blob
  final url = html.Url.createObjectUrlFromBlob(blob);

  // Create an anchor element for downloading the image
  final anchor = html.AnchorElement(href: url)
    ..target = 'blank'
    ..download = 'signature.png'
    ..click();

  // Revoke the URL to release resources
  html.Url.revokeObjectUrl(url);
}
This method is called when the "Save Signature" button is pressed. It captures the signature drawn on the SfSignaturePad, converts it to an image, and then saves it as a PNG file.

await signaturePadKey.currentState!.toImage(): Gets the image representation of the current state of the SfSignaturePad.
await image.toByteData(format: ui.ImageByteFormat.png): Converts the image to ByteData in PNG format.
byteData.buffer.asUint8List(): Converts ByteData to Uint8List.
html.Blob([uint8List]): Creates a Blob from Uint8List.
html.Url.createObjectUrlFromBlob(blob): Creates a URL for the Blob.
html.AnchorElement(href: url)..click(): Creates an anchor element, sets the URL as its href, and triggers a click event to download the image.
html.Url.revokeObjectUrl(url): Revokes the URL to release resources.
</h4>
<h5> A "Blob" (Binary Large Object) is a data structure used to store binary data. In web development, a Blob is often used to represent data that doesn't necessarily fit into a traditional text-oriented format. Blobs can store various types of data, including images, audio, video, and other binary data. </h5>
<h5> Here, html.Blob is a class from the dart:html library (specifically, the web implementation of Dart). It takes a list of data (in this case, a Uint8List, which is an unsigned 8-bit integer list representing binary data) and creates a Blob object.

The Blob is then used to create a URL, and this URL is assigned to the href attribute of an anchor (<a>) element. When the anchor element is clicked programmatically, it triggers the browser to download the data associated with the Blob as a file.</h5>

<h1>Update the UI to Call the Save Method:</h1>
<h4> ElevatedButton(
  onPressed: _saveSignature,
  child: Text('Save Signature'),
),
This button triggers the _saveSignature method when pressed.

By understanding these steps, you can customize the code according to your needs. The key concept is to use the toImage method to capture the drawn signature as an image and then convert and save it as needed.
</h4>



## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
