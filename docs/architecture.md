# Architecture notes

## Main boundary

AegisEye separates biometric acquisition from authorization.

The acquisition layer handles camera and microphone input, detection, quality screening, and versioned experimental descriptors. It does not decide whether a door should open.

The decision layer should evaluate trustworthy identity evidence, authorization rules, liveness, and environmental context. A capture quality score must never be interpreted as a probability of identity.

## Enrollment

1. Obtain explicit consent.
2. Capture a short-lived sample in memory.
3. Reject invalid samples before feature extraction.
4. Create a labeled, versioned descriptor.
5. Protect the descriptor through the existing enrollment service.
6. Write database records and an enrollment audit entry.

Do not log raw samples or keep them in source control.

## Current local research implementation

The local work uses Python, FastAPI, PostgreSQL, SQLAlchemy, Alembic, Fernet, OpenCV, SoundDevice, and Pytest.

Current webcam descriptors are derived from image transforms. Current audio descriptors summarize spectral information. These are processing experiments, not verified face or speaker recognition systems.

## Planned verification work

- Authenticated operator access to enrollment.
- Template lifecycle and revocation.
- Measured genuine and impostor score distributions.
- Presentation-attack and replay tests.
- Liveness challenges with explicit threat assumptions.
- Calibrated decisions in a simulated door environment.
- Audit integrity checks and controlled failure testing.

## Working principle

Record what has actually been tested. Make unknowns visible. Keep acquisition quality, identity confidence, and authorization separate.
