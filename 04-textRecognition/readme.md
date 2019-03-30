# 2. Reconocimiento de Texto

>***Nota:*** Abrir el archivo ***MainActivity.java*** 

### remplazar el codigo

```
private void runTextRecognition() {
    // Replace with code from the codelab to run text recognition.
}
```

por:

```
private void runTextRecognition() {
    FirebaseVisionImage image = FirebaseVisionImage.fromBitmap(mSelectedImage);
    FirebaseVisionTextRecognizer recognizer = FirebaseVision.getInstance()
        .getOnDeviceTextRecognizer();
    mTextButton.setEnabled(false);
    recognizer.processImage(image)
        .addOnSuccessListener(
            new OnSuccessListener<FirebaseVisionText>() {
                @Override
                public void onSuccess(FirebaseVisionText texts) {
                    mTextButton.setEnabled(true);
                    processTextRecognitionResult(texts);
                }
            })
        .addOnFailureListener(
            new OnFailureListener() {
                @Override
                public void onFailure(@NonNull Exception e) {
                    // Task failed with an exception
                    mTextButton.setEnabled(true);
                    e.printStackTrace();
                }
            });
}
```

### remplazar el codigo

```
private void processTextRecognitionResult(FirebaseVisionText texts) {
    // Replace with code from the codelab to process the text recognition result.
}
```

por:

```
private void processTextRecognitionResult(FirebaseVisionText texts) {
    List<FirebaseVisionText.TextBlock> blocks = texts.getTextBlocks();
    if (blocks.size() == 0) {
        showToast("No text found");
        return;
    }
    mGraphicOverlay.clear();
    for (int i = 0; i < blocks.size(); i++) {
        List<FirebaseVisionText.Line> lines = blocks.get(i).getLines();
        for (int j = 0; j < lines.size(); j++) {
            List<FirebaseVisionText.Element> elements = lines.get(j).getElements();
            for (int k = 0; k < elements.size(); k++) {
                Graphic textGraphic = new TextGraphic(mGraphicOverlay, elements.get(k));
                mGraphicOverlay.add(textGraphic);

            }
        }
    }
}
```

## Próximo modulo
Avanzar al [deteccion de rostros](../05-faceDetection)