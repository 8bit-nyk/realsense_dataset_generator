
# RealSense Frame Capture and Metadata Logging

## Description

This Python script captures video streams from an Intel RealSense D435 camera. The script saves the color and depth frames to separate timestamped folders. Additionally, it logs frame metadata, including the frame ID, timestamp, and exposure value, into a text file.

## Dependencies

- Python (Recommended 3.6+)
- `pyrealsense2`: Python bindings for the Intel RealSense SDK 2.0
- `opencv-python`: OpenCV package for Python
- `numpy`: Numerical processing in Python

Install the dependencies using pip:

```bash
pip install pyrealsense2 opencv-python numpy
```

## How the Script Works

### Initial Setup

1. **Timestamp Generation**: A timestamp is generated based on the current system time in the format `YYYYMMDD_HHMMSS`. This timestamp is then used to name the output folders and metadata text file.
2. **Directory Creation**: Two directories are created — one for color images and another for depth images. The directory names are prefixed with `color_images_` and `depth_images_`, followed by the timestamp.
3. **Metadata File**: A text file named `frame_metadata_TIMESTAMP.txt` is created to store metadata for each frame.

### Camera Configuration

1. **Alignment Object**: An alignment object is created to ensure that the depth frames are aligned to the color frames.
2. **Stream Configuration**: The script configures the camera to capture both depth and color streams at a resolution of 640x480 pixels and 30 frames per second.
3. **Streaming**: The script initializes the camera's pipeline and starts streaming.

### Frame Processing and Storage

Within a loop:

1. The script waits for new frames from the camera.
2. It aligns the depth frames to the color frames.
3. If either the color or aligned depth frame is not available, the script skips the current iteration.
4. The script converts the raw frame data into numpy arrays.
5. The color frames are saved as JPEG files in the color images directory.
6. The depth frames are saved as PNG files in the depth images directory.
7. The script logs the frame number, UNIX timestamp (in seconds), and exposure value (in milliseconds) to the metadata text file.
8. Optionally, the color and depth images are displayed in real-time using OpenCV. You can close the windows by pressing `q`.

### Cleanup

Once the script ends (either due to an error or manual termination), the camera pipeline is stopped, the metadata text file is closed, and any OpenCV windows are destroyed.

## Output Structure

1. **Color Images Directory (`color_images_TIMESTAMP`)**:
   - Contains JPEG images of color frames.
   - Filenames follow a 6-digit format, such as `000001.jpg`, `000002.jpg`, etc.

2. **Depth Images Directory (`depth_images_TIMESTAMP`)**:
   - Contains PNG images of depth frames.
   - Filenames mirror those in the color images directory, e.g., `000001.png`, `000002.png`, etc.

3. **Metadata Text File (`frame_metadata_TIMESTAMP.txt`)**:
   - Each line corresponds to a single frame.
   - Fields are separated by commas in the following order:
     1. Frame ID (6-digit format, e.g., `000001`)
     2. UNIX timestamp (in seconds since the UNIX epoch)
     3. Exposure value (in milliseconds)

## Usage

To use the script, simply run:

```bash
python script_name.py
```

Replace `script_name.py` with the filename of the script.

Note: For optimal performance, especially when capturing at high frame rates, consider commenting out the real-time display of frames using OpenCV.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
