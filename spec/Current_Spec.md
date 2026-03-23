# Petmory Current Spec (SSOT v1.0)

## 1. Core Concept
- Memory = 1 Photo
- Emotion = Enum
- AI runs automatically on memory creation

---

## 2. Emotion Enum

- happy
- grateful
- proud
- miss
- sad
- comforted

---

## 3. Database Schema

### users
- id (UUID)
- email (TEXT)
- password_hash (TEXT)
- created_at (TIMESTAMP)

### pets
- id (UUID)
- user_id (UUID)
- name (TEXT)
- species (TEXT)
- breed (TEXT, nullable)
- date_of_passing (DATE, nullable)
- profile_image_url (TEXT, nullable)
- created_at (TIMESTAMP)

### memories
- id (UUID)
- user_id (UUID)
- pet_id (UUID)
- photo_url (TEXT)
- ai_context (TEXT)
- ai_narrative (TEXT)
- emotion (ENUM)
- created_at (TIMESTAMP)

### conversations
- id (UUID)
- user_id (UUID)
- type (memory | together)
- created_at (TIMESTAMP)

### messages
- id (UUID)
- conversation_id (UUID)
- sender_type (user | pet)
- pet_id (UUID, nullable)
- content (TEXT)
- created_at (TIMESTAMP)

---

## 4. API Rules

### Memory Creation
- POST /memories
- Input: petId, photoUrl, emotion
- Server MUST:
  - generate ai_context
  - generate ai_narrative
  - save memory

---

## 5. Constraints

- No multi-photo memory
- No custom emotion
- No group conversation (MVP)
- No notification system (MVP)
