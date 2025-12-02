# No-JS Parity Verification Script — Week 8

**Purpose**: Verify all task flows work identically with JavaScript disabled.

**Setup**:
1. Open browser DevTools → Settings → Disable JavaScript
2. Hard refresh (Ctrl+Shift+R / Cmd+Shift+R)

---

## Test 1: Add Task (Success Case)

**Steps**:
1. Navigate to `/tasks`
2. Enter title "No-JS test task"
3. Click "Add Task"

**Expected**:
- Full page reload
- New task appears in list
- URL remains `/tasks`
- No error messages

**Result**: [ ] Pass  [ ] Fail

---

## Test 2: Add Task (Validation Error)

**Steps**:
1. Leave title field empty
2. Click "Add Task"

**Expected**:
- Full page reload
- URL shows `/tasks?error=title`
- Error summary appears at top
- Input has `aria-invalid="true"`

**Result**: [ ] Pass  [ ] Fail

---

## Test 3: Filter Tasks

**Steps**:
1. Add tasks "Alpha", "Bravo", "Charlie"
2. Enter "ra" in filter box
3. Click "Apply" button

**Expected**:
- Full page reload
- URL shows `/tasks?q=ra&page=1`
- Only "Bravo" and "Charlie" visible

**Result**: [ ] Pass  [ ] Fail

---

## Test 4: Pagination

**Steps**:
1. Add 15 tasks
2. Click "Next" link

**Expected**:
- Full page reload
- URL shows `/tasks?page=2`
- Tasks 11-15 visible
- "Previous" link appears

**Result**: [ ] Pass  [ ] Fail

---

## Test 5: Delete Task

**Steps**:
1. Click "Delete" button on a task

**Expected**:
- Form submits to `POST /tasks/{id}/delete`
- Full page reload
- Task removed from list
- **No confirmation dialog** (documented trade-off)

**Result**: [ ] Pass  [ ] Fail

---

## Test 6: Keyboard Navigation

**Steps**:
1. Tab through entire page
2. Press Enter on "Add Task"
3. Tab to error link, press Enter

**Expected**:
- Focus order matches visual order
- All interactive elements reachable
- Error link moves focus to input

**Result**: [ ] Pass  [ ] Fail

---

## Test 7: Browser History

**Steps**:
1. Start at `/tasks`
2. Filter to "test"
3. Go to page 2
4. Click browser Back button twice

**Expected**:
- Back #1 → filtered, page 1
- Back #2 → unfiltered

**Result**: [ ] Pass  [ ] Fail

---

## Summary

**Passed**: _____ / 7
**Failed**: _____ / 7

**Issues found**: (log in `wk08/backlog/issues.csv`)

**Evidence**: Capture screenshots in `wk08/evidence/nojs-parity/`

---

**Verified by**: __________
**Date**: __________
