# AegisEye

**Risk-aware biometric authentication and secure access control**

AegisEye is a research project I'm building to understand how face, eye, and voice evidence can work together in an access control system. The idea is to look beyond a simple biometric match and examine the harder questions: Was the sample captured properly? Can the evidence be trusted? Does the person have permission to enter? What should happen when signals disagree?

My interest in this work grew from studying cybersecurity at Bayero University Kano, Nigeria, and spending more time building software. I enjoy the engineering side of security, particularly turning threat models and security requirements into systems I can test, break, and improve.

This project is still being developed. I document the decisions, limitations, and progress rather than treating a working demonstration as proof that the system is secure.

## What I've built locally

The current local prototype includes:

- A Python backend using FastAPI.
- PostgreSQL persistence using SQLAlchemy and Alembic migrations.
- User enrollment with encrypted experimental biometric templates.
- Duplicate-reference checks and enrollment audit records.
- Policy and risk evaluation designed for multiple evidence sources.
- Webcam acquisition, face and eye detection, and image quality checks using OpenCV.
- Microphone capture, audio quality assessment, and experimental voice features.
- Command-line demonstrations and automated tests.

**Repository status:** The local project source has not yet been committed here. This repository begins with documentation while the working code is prepared for a separate, security-reviewed upload.

## Architecture

```text
Camera / Microphone
        |
        v
Face, eye, and voice acquisition
        |
        v
Quality checks
        |
        v
Experimental feature extraction
        |
        v
Template protection
        |
        v
Enrollment service
        |
        v
PostgreSQL + audit trail
```

Enrollment and authentication are intentionally separate concerns. Accepting a clear image or audible recording does not prove someone's identity.

The intended authentication flow is:

```text
Biometric and contextual evidence
        |
        v
Evidence validation and security policy
        |
        v
Risk assessment and multi-modal fusion
        |
        v
Explainable access decision
        |
        v
Door simulator + audit trail
```

The second flow is a design direction, not a claim that end-to-end biometric verification and door control are already validated.

## Technology

| Responsibility | Technology |
| --- | --- |
| Backend | Python 3.11, FastAPI |
| Database | PostgreSQL, SQLAlchemy |
| Migrations | Alembic |
| Webcam processing | OpenCV, NumPy |
| Microphone acquisition | SoundDevice, NumPy |
| Template protection | Cryptography, Fernet |
| Testing | Pytest |
| Local services | Docker Compose |

## Running the local project

These commands describe the local development setup. They will become executable from a fresh clone after the application source is published.

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m pytest -q
```

Camera validation:

```powershell
.\.venv\Scripts\python.exe -m scripts.capture_face_eye
```

Voice quality validation:

```powershell
.\.venv\Scripts\python.exe -m scripts.capture_voice --mode validate
```

Combined experimental enrollment:

```powershell
.\.venv\Scripts\python.exe -m scripts.capture_voice --mode multimodal
```

The camera and microphone experiments require explicit consent and should be used with test identities in a trusted development environment.

## Security boundaries

AegisEye is a research prototype, not a production biometric authentication system.

- The current face, eye, and voice descriptors are experimental. They are not validated identity embeddings.
- A quality check does not demonstrate liveness or defeat replay and presentation attacks.
- An exact-reference duplicate check does not establish that two different captures belong to the same person.
- Enrollment authorization and template lifecycle management need further hardening.
- No experimental biometric score should be used to unlock a real door.
- Raw biometric recordings, images, datasets, encryption keys, database credentials, and `.env` files must stay out of the repository.

Security claims will need controlled testing and measurable results before they are made.

## What comes next

I'm working toward authenticated enrollment, better identity management, versioned matching interfaces, liveness and replay testing, calibrated multi-modal fusion, and an audited door access simulator.

The goal is to build an understandable system with clear security boundaries, not just an impressive-looking recognition demo.

## Author

**Abdurrahman Suleiman**

Cybersecurity studies at Bayero University Kano, Nigeria. Interested in software engineering, applied AI, and secure systems.

GitHub: [@Realavdulmouhd](https://github.com/Realavdulmouhd)

## Status

Active development. Source publication is pending a review of secrets, biometric data, and local configuration.
