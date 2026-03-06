# Face Recognition Attendance System

A comprehensive, intelligent attendance management system powered by facial recognition technology. This project automates the attendance marking process using deep learning and computer vision, eliminating the need for manual roll calls or card-based systems. The system features a user-friendly GUI, secure admin authentication, and advanced data analytics capabilities.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technical Architecture](#technical-architecture)
- [Requirements](#requirements)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
- [Database Schema](#database-schema)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## 🎯 Overview

The Face Recognition Attendance System is a Python-based application that leverages state-of-the-art facial recognition algorithms to automatically mark attendance. It combines OpenCV for video capture, face_recognition library for face detection and matching, SQLite for persistent data storage, and Tkinter for an intuitive graphical interface.

**Key Benefits:**
- 🚀 Fully automated attendance marking
- 🔒 Secure admin-only access with authentication
- 📊 Real-time analytics and visualization
- 💾 Persistent database storage
- 📁 Easy CSV export for further analysis
- 🖥️ Cross-platform compatibility (Windows, macOS, Linux)

## ✨ Features

### Core Functionality
- **Facial Recognition**: Automatically detects and recognizes faces from webcam feed
- **Real-time Processing**: Processes video stream at 30+ FPS with efficient resizing
- **Auto-Attendance Marking**: Marks attendance once per day per student
- **Duplicate Prevention**: Ensures a student's attendance is recorded only once per day

### User Management
- **Admin Login System**: Secure authentication to prevent unauthorized access
- **Add New Students**: Capture and store student facial images with one-click enrollment
- **Student Database**: Maintains a database of recognized students with their images

### Data Management
- **SQLite Database**: Stores all attendance records with timestamp precision
- **View Attendance**: Browse all attendance records in a tabular format
- **Export to CSV**: Export attendance data for Excel analysis or reporting
- **Data Visualization**: Generate bar charts showing attendance trends over time
- **Bulk Erase**: Clear attendance records with confirmation prompt

### User Interface
- **Graphical User Interface (GUI)**: Built with Tkinter for easy interaction
- **Real-time Video Feed**: Live video display with face detection overlays
- **Status Messages**: Provides feedback on all operations
- **Responsive Design**: Intuitive button layout and clear instructions

## 🏗️ Technical Architecture

### Technology Stack
- **Python 3.7+**: Core programming language
- **OpenCV (cv2)**: Video capture and image processing
- **face_recognition**: Deep learning for face detection and comparison
- **dlib**: Underlying face recognition engine
- **SQLite3**: Lightweight relational database
- **Tkinter**: Cross-platform GUI framework
- **Pillow (PIL)**: Image processing for GUI display
- **Matplotlib**: Data visualization and charting
- **NumPy**: Numerical computing and array operations

### Face Recognition Process

1. **Image Preparation**: Load reference images from `ImagesAttendance` folder
2. **Encoding Generation**: Convert each image to 128-dimensional face encoding
3. **Video Capture**: Stream video from webcam at 25% resolution for speed
4. **Face Detection**: Identify face locations in each frame
5. **Face Comparison**: Compare detected faces against known encodings
6. **Distance Calculation**: Calculate Euclidean distance (0 = perfect match)
7. **Matching**: If distance is below threshold, mark as recognized

## 📦 Requirements

### System Requirements
- **Python**: 3.7 or higher
- **Camera**: Built-in or external webcam
- **Storage**: Minimum 500MB free space for database and images
- **RAM**: Minimum 2GB recommended

### Python Dependencies

```
opencv-python>=4.5.0
face-recognition>=1.3.0
Pillow>=8.0.0
matplotlib>=3.3.0
numpy>=1.19.0
dlib>=19.0
```

## 🔧 Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/Sandip7224/face-Recognition-Attendance-Project.git
cd face-Recognition-Attendance-Project
```

### Step 2: Create Virtual Environment (Recommended)

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

Or install packages individually:

```bash
pip install opencv-python
pip install face-recognition
pip install Pillow
pip install matplotlib
pip install numpy
```

### Step 4: Setup ImagesAttendance Folder

```bash
mkdir ImagesAttendance
```

This folder must contain reference images of all individuals to be recognized.

### Step 5: Run the Application

```bash
python main.py
```

## 📂 Project Structure

```
face-Recognition-Attendance-Project/
│
├── main.py                          # Main application file
├── ImagesAttendance/                # Folder for reference images
│   ├── john_doe.jpg
│   ├── jane_smith.jpg
│   └── ...
├── attendance.db                    # SQLite database (auto-created)
├── attendance_export.csv            # Exported attendance records
├── README.md                        # This file
└── requirements.txt                 # Python dependencies
```

## 📖 Usage Guide

### First Launch

1. **Start the Application**
   ```bash
   python main.py
   ```

2. **Login Screen Appears**
   - Default Username: `admin`
   - Default Password: `password`
   - Click "Login" button

3. **Main Dashboard Opens**
   - Video feed displays on the right
   - Control buttons on the left sidebar

### Adding New Students

1. Click **"Add New Student"** button
2. Enter the student's name in the text field
3. Camera preview appears in the window
4. Click **"Add Student"** to capture the facial image
5. Image is saved to `ImagesAttendance/StudentName.jpg`
6. Close the window to return to main screen

### Starting Attendance

1. Click **"Start Attendance"** button
2. System loads all reference images and generates encodings
3. Camera feed starts streaming in real-time
4. Recognized students are highlighted with green rectangles
5. Names appear above the rectangles
6. Attendance is automatically marked in the database

### Viewing Attendance Records

1. Click **"View Attendance"** button
2. New window opens showing a table with:
   - Student Name
   - Date (YYYY-MM-DD format)
   - Time (HH:MM:SS format)
3. Scroll through all records in the table

### Exporting Data

1. Click **"Export to CSV"** button
2. Attendance records are saved to `attendance_export.csv`
3. File can be opened in Excel or any spreadsheet application

### Visualizing Data

1. Click **"Visualize Data"** button
2. A bar chart appears showing:
   - X-axis: Dates
   - Y-axis: Number of students marked present
   - Trend analysis of attendance over time

### Stopping Attendance

1. Click **"Stop Attendance"** button
2. Webcam feed stops
3. System displays: "Number of students present today: X out of Y"
4. Console shows summary statistics

### Erasing Records

1. Click **"Erase Attendance"** button
2. Confirmation dialog appears
3. Click "OK" to permanently delete all records
4. Or "Cancel" to abort the operation

## 🗄️ Database Schema

### Attendance Table Structure

```sql
CREATE TABLE IF NOT EXISTS attendance (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    date TEXT NOT NULL,
    time TEXT NOT NULL
)
```

### Column Details
- **id**: Unique identifier for each record (auto-incremented)
- **name**: Student's name (stored in uppercase)
- **date**: Date of attendance in YYYY-MM-DD format
- **time**: Time of attendance in HH:MM:SS format

### Sample Data
```
| id | name        | date       | time     |
|----|-------------|------------|----------|
| 1  | JOHN_DOE    | 2024-01-15 | 09:30:45 |
| 2  | JANE_SMITH  | 2024-01-15 | 09:32:10 |
| 3  | JOHN_DOE    | 2024-01-16 | 09:28:30 |
```

## ⚙️ Configuration

### Change Admin Credentials

Edit `main.py` (around line 227):

```python
if username == "admin" and password == "password":
```

Change to your desired credentials:

```python
if username == "your_username" and password == "your_password":
```

### Adjust Face Recognition Sensitivity

In the `start_attendance()` function, modify the matching threshold:

```python
# Lower value = stricter matching (fewer false positives)
# Higher value = lenient matching (more false positives)
if matches[matchIndex]:  # Default: simple boolean
```

### Adjust Video Capture Resolution

In `start_attendance()` function (line 95):

```python
# Current: 25% resolution for speed
imgS = cv2.resize(img, (0, 0), None, 0.25, 0.25)

# Change to 0.5 for better accuracy but slower processing
imgS = cv2.resize(img, (0, 0), None, 0.5, 0.5)
```

## 🐛 Troubleshooting

### Issue: "Could not open webcam"

**Solution:**
- Check if camera is connected and not in use by another application
- Verify camera permissions in system settings
- Try using a different camera port (modify `cv2.VideoCapture(0)` to `cv2.VideoCapture(1)`)

### Issue: "Face not found in image"

**Solution:**
- Ensure images in `ImagesAttendance` folder clearly show face
- Remove low-quality or blurry images
- Ensure images are in JPG or PNG format
- Re-add the student with a clearer image

### Issue: Faces not being recognized

**Solution:**
- Check lighting conditions are adequate
- Ensure student is facing camera directly
- Adjust distance from camera (30-60cm optimal)
- Check if reference image quality matches current lighting
- Verify face recognition is loaded (check console for "Encoding Complete")

### Issue: Database locked error

**Solution:**
- Close any other instances of the application
- Delete `attendance.db` and restart application
- Check file permissions on the project directory

### Issue: High CPU usage

**Solution:**
- Reduce video frame resolution
- Lower frame rate by increasing `after()` delay
- Close other applications
- Use a simpler reference image set

### Issue: Tkinter not found

**Solution:**

Windows:
```bash
python -m pip install tk
```

Ubuntu/Debian:
```bash
sudo apt-get install python3-tk
```

macOS:
```bash
brew install python-tk@3.9  # or your Python version
```

## 🤝 Contributing

We welcome contributions to improve this project! Here's how you can get involved:

### Steps to Contribute

1. **Fork the Repository**
   ```bash
   Click the "Fork" button on GitHub
   ```

2. **Create a Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Your Changes**
   - Ensure code follows PEP 8 style guide
   - Add comments for complex logic
   - Test thoroughly before committing

4. **Commit Your Changes**
   ```bash
   git commit -m 'Add feature: brief description'
   git commit -m 'Fix: bug description'
   ```

5. **Push to Your Branch**
   ```bash
   git push origin feature/your-feature-name
   ```

6. **Open a Pull Request**
   - Describe your changes clearly
   - Reference any related issues
   - Wait for review and approval

### Areas for Contribution
- Improved face recognition accuracy
- Performance optimization
- Additional data visualization options
- Enhanced error handling
- Support for multiple cameras
- Mobile app companion
- Docker containerization
- Unit and integration tests

## 📄 License

This project is open source and available under the MIT License. See LICENSE file for details.

## 📧 Contact

For questions, suggestions, or collaboration inquiries, feel free to reach out:

**Project Maintainer:** Sandip Gupta

- **Email:** sandip1352005gupta@gmail.com
- **LinkedIn:** [Sandeep Gupta](https://www.linkedin.com/in/sandeep-gupta-b74956294/)
- **GitHub:** [Sandip7224](https://github.com/Sandip7224)

## 🚀 Future Enhancements

Potential features for future versions:
- [ ] Multi-face recognition in single frame
- [ ] Real-time attendance summary dashboard
- [ ] Email notifications for absences
- [ ] Facial expression analysis
- [ ] Integration with Google Sheets/Forms
- [ ] Mobile app for remote access
- [ ] QR code integration
- [ ] Biometric template encryption
- [ ] Advanced reporting and analytics
- [ ] Support for multiple departments

## 📚 Resources

- [Face Recognition Library Documentation](https://github.com/ageitgey/face_recognition)
- [OpenCV Documentation](https://docs.opencv.org/)
- [Tkinter Tutorial](https://docs.python.org/3/library/tkinter.html)
- [SQLite Documentation](https://www.sqlite.org/docs.html)

## ⭐ Acknowledgments

Special thanks to:
- Adam Geitgey for the excellent face_recognition library
- OpenCV community for computer vision tools
- Python community for amazing libraries and support

---

**Last Updated:** March 2026

**Status:** Active Development

**Contributors:** Sandip Gupta and the open-source community
