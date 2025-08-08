Bug Report Summary
### Duplicate Email Sending
**File**: LeadCaptureForm.tsx (lines 30–66)
**Severity**: Critical
**Status**: Fixed
#### Problem
The confirmation email function is called twice, at lines 30–46 and again at 49–65, causing
duplicate emails to be sent to users.
#### Root Cause
Redundant function invocation without proper flag or state separation.
#### Fix
Removed the second invocation and ensured the confirmation function is called only once per
submission.
#### Impact
✔ Single confirmation email sent per submission
✔ Improved user experience
✔ No duplicate leads in CRM
### Wrong Array Index in AI Function
**File**: send-confirmation/index.ts (line 45)
**Severity**: Critical
**Status**: Fixed
#### Problem
`data?.choices[1]?.message?.content` was used instead of `data?.choices[0]?.message?.content`.
OpenAI API returns the first choice at index 0.
#### Root Cause
Incorrect assumption about API response indexing.
#### Fix
Changed index from `[1]` to `[0]` to correctly retrieve AI content.
#### Impact
✔ Correct AI content is now shown
✔ Avoids fallback message usage
### State Management Bug
**File**: LeadCaptureForm.tsx
**Severity**: Critical
**Status**: Fixed
#### Problem
Mix of local state and Zustand store caused state desync. Form bypassed `addLead` function from
the store.
#### Root Cause
Inconsistent use of shared and local state stores.
#### Fix
Refactored form to exclusively use Zustand `addLead` for state updates.
#### Impact
✔ Synced state across UI
✔ Accurate success counts
### Interface Mismatch
**File**: lead-store.ts
**Severity**: Critical
**Status**: Fixed
#### Problem
Lead interface missing `industry` field; form attempted to store it, causing inconsistency.
#### Root Cause
Lead interface not updated with expected fields.
#### Fix
Added `industry` to the Lead interface.
#### Impact
✔ Type-safe form handling
✔ No more silent data drops
### Missing Database Persistence
**File**: LeadCaptureForm.tsx
**Severity**: Major
**Status**: Fixed
#### Problem
Lead form data was only stored in local state and not persisted to Supabase.
#### Root Cause
No call to Supabase insert method after form submission.
#### Fix
Integrated Supabase insert logic after successful form submission.
#### Impact
✔ Leads now saved to backend
✔ Survives page reloads
### React Router Deprecation Warnings
**File**: package.json / Router setup
**Severity**: Minor
**Status**: Fixed
#### Problem
Deprecation warnings for missing v7 future flags: `startTransition`, `relativeSplatPath`.
#### Root Cause
Router setup missing required future config flags.
#### Fix
Added required future flags to router config.
#### Impact
✔ Clean console output
✔ Future-proof routing setup
### Unused useEffect
**File**: LeadCaptureForm.tsx (lines 17–19)
**Severity**: Minor
**Status**: Fixed
#### Problem
Redundant `useEffect` that sets `setSubmitted(false)` on mount only.
#### Root Cause
Leftover effect from earlier implementation.
#### Fix
Removed unused useEffect block.
#### Impact
✔ Cleaner component lifecycle
✔ No redundant render