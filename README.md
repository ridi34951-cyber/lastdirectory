# GyroLock V13 — Counter-Motion Gyro XYZ + Live Preview

This project keeps gyro XYZ stabilization and adds a lightweight live gyro-stabilized camera preview.

## Changes in V13
- Live preview uses counter-motion: the preview transform moves opposite the measured phone rotation, instead of visually following the phone.
- Small movements are countered immediately; correction is limited to a crop-safe range, then the frame can show some movement after reaching that limit. A slow follow keeps the correction from staying pinned forever.
- Reduced the live preview dead-band and improved response smoothing to react to smaller movements without making sensor noise excessively visible.
- Recording still captures the camera stream and then applies gyro XYZ stabilization to the saved video after recording stops. The view transform itself is not the encoded video stream.
- More responsive post-stabilization: correction gain 0.90, lower dead-band (0.009 rad/s), and a 75 ms gyro low-pass filter.
- Shorter 0.90 s trajectory smoothing window to make stabilization more visible while keeping small high-frequency sensor noise suppressed.
- Correction limits prevent extreme tilts from causing excessive frame jumps or edge exposure.
- Original recording is preserved; processed video is saved separately under Movies/GyroLock.
- Output targets 30 FPS and uses the existing MPEG-4 encoder command without unsupported `-preset` options.

## Build
Upload the contents of this ZIP to the root of a GitHub repository, then run the `Build GyroLock APK` workflow under Actions. Download the `GyroLock-debug-apk` artifact after a successful build.

## Testing notes
Archive integrity is checked, but this project has not been compiled or tested on a physical phone in this environment. Test with a short clip first. Live preview stabilization is a lightweight 2D transform; the saved output receives the gyro-based FFmpeg pass after recording.
