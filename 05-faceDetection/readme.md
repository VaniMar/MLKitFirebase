# 2. Reconocimiento de Rostros

>***Nota:*** Abrir el archivo ***MainActivity.java*** 

### remplazar el codigo

```
private void runFaceContourDetection() {
    // Replace with code from the codelab to run face contour detection.
}
```

por:

```
private void runFaceContourDetection() {
    FirebaseVisionImage image = FirebaseVisionImage.fromBitmap(mSelectedImage);
    FirebaseVisionFaceDetectorOptions options =
        new FirebaseVisionFaceDetectorOptions.Builder()
                .setPerformanceMode(FirebaseVisionFaceDetectorOptions.FAST)
                .setContourMode(FirebaseVisionFaceDetectorOptions.ALL_CONTOURS)
                .build();

    mFaceButton.setEnabled(false);
    FirebaseVisionFaceDetector detector = FirebaseVision.getInstance().getVisionFaceDetector(options);
    detector.detectInImage(image)
        .addOnSuccessListener(
        new OnSuccessListener<List<FirebaseVisionFace>>() {
            @Override
            public void onSuccess(List<FirebaseVisionFace> faces) {
                mFaceButton.setEnabled(true);
                processFaceContourDetectionResult(faces);
            }
        })
        .addOnFailureListener(
        new OnFailureListener() {
            @Override
            public void onFailure(@NonNull Exception e) {
                // Task failed with an exception
                mFaceButton.setEnabled(true);
                e.printStackTrace();
            }
        });
}
```

### remplazar el codigo

```
private void processFaceContourDetectionResult(List<FirebaseVisionFace> faces) {
    // Replace with code from the codelab to process the face contour detection result.
}
```

por:

```
private void processFaceContourDetectionResult(List<FirebaseVisionFace> faces) {
    // Task completed successfully
    if (faces.size() == 0) {
        showToast("No face found");
        return;
    }
    mGraphicOverlay.clear();
    for (int i = 0; i < faces.size(); ++i) {
        FirebaseVisionFace face = faces.get(i);
        FaceContourGraphic faceGraphic = new FaceContourGraphic(mGraphicOverlay);
        mGraphicOverlay.add(faceGraphic);
        faceGraphic.updateFace(face);
    }
}
```

## Próximo modulo
Avanzar al [deteccion de objetos](../06-FindObjects)
