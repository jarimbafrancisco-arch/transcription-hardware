docs: confirm Gemini API workflow and update integration guides

BREAKING CHANGE: Summarization is now user-triggered only (not automatic)

This commit updates all integration documentation to reflect the confirmed
implementation workflow using Google Gemini API for transcription and
on-demand summarization.

## Changes

### AI Integration Guide
- Updated data flow to show confirmed workflow: ESP32 → Supabase Storage → 
  Gemini transcription → User-triggered summarization
- Removed speculative implementation options, confirmed Gemini 1.5 Pro for 
  transcription and summarization
- Added Supabase Storage setup requirements section
- Updated transcription processing to handle audio from Supabase Storage URLs
- Added API endpoint example for on-demand summarization (FastAPI)
- Clarified that summarization only happens when user clicks button in UI

### Hardware Integration Guide
- Added Supabase Storage setup section with bucket creation and policies
- Replaced old sendNote() function with complete audio upload workflow
- Added saveAudioToFile(), uploadAudioToStorage(), and createNoteWithAudio() 
  functions
- Updated recordAndUploadAudio() to show complete workflow
- Added SPIFFS initialization for local file storage
- Updated overview to emphasize audio upload to Supabase Storage

### Frontend Integration Guide
- Added "Generate Summary" section with API call example
- Added React component example for summarization button
- Clarified that summarization is user-triggered, not automatic
- Added TypeScript examples for calling /api/summarize endpoint

### Database Design Documentation
- Added "Confirmed System Workflow" section with step-by-step flow diagram
- Updated example ESP32 inserts to show audio_file_url instead of text
- Added note about automatic transcription update via background job
- Clarified that summarization is on-demand only (user-triggered)

## Supabase Setup Requirements

Documentation now includes:
1. Storage bucket setup (audio bucket with public access)
2. Storage policies for service role and public access
3. Background job requirements for automatic transcription
4. API endpoint requirements for user-triggered summarization

## Workflow Confirmation

Confirmed workflow:
1. ESP32 records audio → Uploads to Supabase Storage
2. ESP32 creates note with audio_file_url (text is NULL initially)
3. Background job transcribes audio using Gemini API
4. User clicks "Summarize" button in UI → Triggers summarization API
5. Summary saved to database

All documentation now consistently reflects this confirmed implementation.

