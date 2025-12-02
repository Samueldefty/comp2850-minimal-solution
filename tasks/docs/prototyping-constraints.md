# Prototyping Constraints & Trade-offs

## Rendering splits
- Full page: [describe what `/tasks` returns and when it's used]
- Fragment: [describe what `/tasks/fragment` returns and when it's used]

## URL & History
- [Explain how `hx-push-url="true"` maintains browser history]
- [What breaks if you remove it?]

## Accessibility hooks
- [Describe the live region `#status` and its purpose]
- [Explain `aria-describedby` connection between list and result count]
- [Why is result count visually hidden?]

## State management
- [How do query parameters (`q`, `page`) maintain state?]
- [Why must pagination links include the filter query?]

## Performance notes
- Page size: [your choice - justify it]
- Fragment response size vs full page: [estimate bandwidth savings]
- Debounce delay: [300ms - why this value?]

## Future risks
- [What could go wrong with this approach?]
- [Scalability concerns (e.g., 10,000 tasks)?]
- [Template maintenance burden?]

## Accessibility verification

### Keyboard testing
- [Results from Tab navigation test]

### Screen reader testing
- [If available: what was announced when filtering?]

### No-JS parity
- [Confirmation that all features work without JavaScript]






## Dual-Path Architecture (Lab 2)

### Design Decision
Every route handles both HTMX (enhanced) and no-JS (baseline) requests.

### Benefits
- Works for everyone regardless of JS availability
- Resilience if JS fails to load
- Testing baseline proves server-first architecture

### Costs
- Code complexity (conditional logic in every route)
- Testing burden (two paths per feature)
- Template maintenance

### Mitigations
- Shared partials (`_item.peb`, `_list.peb`)
- Verification script (`scripts/nojs-check.md`)
- Backlog tracking for parity issues

---

## Validation Strategy

### Design Decision
All validation on server. No client-side enforcement.

### Benefits
- Security (client-side can be bypassed)
- Consistency across HTMX/no-JS paths
- Accessible error responses

### Costs
- Latency (round-trip for validation)
- No instant feedback

### Mitigations
- Clear error messages (WCAG 3.3.1)
- `aria-invalid`, `aria-describedby` for screen readers
- Focus management (error link → input)

---

## Delete Confirmation Trade-off

### Design Decision
HTMX uses `hx-confirm`. No-JS has no confirmation.

### Risk
People might accidentally delete tasks in no-JS mode.

### Mitigation
- Documented in constraints doc
- Backlog item: consider adding `/tasks/{id}/delete/confirm` page
- Future: "Undo" feature (restore from soft-delete)

---

## Evidence

**Verification script**: `wk08/scripts/nojs-check.md`
**Test results**: [7/7 passed - date]
**Evidence folder**: `wk08/evidence/nojs-parity/`
**Backlog items**: wk8-01 (delete confirmation), wk8-02 (...)
