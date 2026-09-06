<div align="center">
  <h1>📸 SnapClass</h1>
  <p><b>Making Attendance faster using AI</b></p>
  
  [![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://streamlit.io/)
  [![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
  [![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white)](https://supabase.com/)
  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
</div>

<br />

SnapClass is a next-generation attendance management system designed for educators. By leveraging cutting-edge **Facial Recognition** and **Voice Biometrics**, it automates roll calls, reducing administrative overhead and preventing proxy attendance.

---

## ✨ Key Features

### 🎓 For Teachers
- **Automated Facial Attendance**: Upload a group photo of the classroom. SnapClass uses `dlib` and an SVM classifier to identify multiple faces in the crowd simultaneously and mark them present.
- **Voice/Audio Attendance**: Upload a continuous audio recording (e.g., students saying "present"). SnapClass uses speaker diarization and `Resemblyzer` to verify students based on their unique voice embeddings.
- **Subject Management**: Create classrooms, manage students, and generate shareable join links and QR codes.
- **Analytics & Logs**: Track total classes held and monitor student attendance history.

### 🧑‍🎓 For Students
- **Smart Enrollment**: One-click enrollment using teacher-provided join links or QR codes.
- **Biometric Profiles**: Securely register face and voice samples directly from the dashboard.
- **Attendance Tracking**: View enrolled subjects and track personal attendance records seamlessly.

---

## 🏗️ Architecture & Tech Stack

SnapClass is built with a modular architecture, prioritizing clean separation between UI, ML pipelines, and database interactions.

- **Frontend Framework**: [Streamlit](https://streamlit.io/)
- **Backend & Database**: [Supabase](https://supabase.com/) (PostgreSQL + Auth)
- **Face Recognition Pipeline**: `dlib`, `face_recognition`, `scikit-learn` (SVM)
- **Voice Recognition Pipeline**: `Resemblyzer`, `librosa`
- **Utilities**: `bcrypt` (password hashing), `segno` (QR codes), `pillow`, `numpy`, `pandas`

---

## 📂 Project Structure

```text
snapclass/
├── .streamlit/             # Streamlit configuration and secrets
├── src/                    # Source code directory
│   ├── components/         # Reusable UI components & dialogs (e.g., auto_enroll)
│   ├── database/           # Supabase connection & DB controllers (db.py)
│   ├── pipelines/          # AI logic (face_pipelines.py, voice_pipeline.py)
│   ├── screens/            # Main application screens (Home, Teacher, Student)
│   └── ui/                 # Base layout configurations
├── app.py                  # Application entry point
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

1. **Python 3.10+** installed on your machine.
2. **C++ Build Tools**: Required to compile `dlib`. 
   - *Windows*: Install Visual Studio C++ Build Tools.
   - *macOS/Linux*: Install `cmake` and `gcc`.
3. **Supabase Project**: A Supabase project with tables properly set up (see Database Schema below).

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/kartik14964/snapclass.git
   cd snapclass
   ```

2. **Set up a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Environment Variables**
   Create a `.streamlit/secrets.toml` file in the root directory:
   ```toml
   SUPABASE_URL = "your-supabase-url"
   SUPABASE_KEY = "your-supabase-service-role-key"
   ```

### 🗄️ Database Schema Outline
*You will need the following tables in your Supabase project to run the application natively:*
- `teachers` (id, username, password, name)
- `students` (student_id, name, face_embedding, voice_embedding)
- `subjects` (id, subject_code, name, section, teacher_id)
- `subject_students` (student_id, subject_id)
- `attendance_logs` (id, student_id, subject_id, timestamp)

---

## 🎮 Usage

Start the Streamlit server:
```bash
streamlit run app.py
```
*The app will be available at `http://localhost:8501`.*

- **Login**: Choose whether you are logging in as a Teacher or a Student.
- **Teacher View**: Create a subject -> Share the join code with students -> Once students register their biometrics, use the **Add Photo** or **Voice Attendance** dialogs to take attendance.
- **Student View**: Sign up -> Complete biometric profile -> Enroll via Join Code.

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve the accuracy of the ML models, enhance the UI, or fix bugs:
1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.

<div align="center">
  <i>Built with ❤️ for a smarter classroom experience.</i>
</div>
